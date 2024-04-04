---
layout: default
title: Kafka Producer
parent: Kafka
nav_order: 3
---
### Kafka producer example 
`build.gradle`
```groovy
plugins {
	id 'java'
	id 'org.springframework.boot' version '3.1.1'
	id 'io.spring.dependency-management' version '1.1.0'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	sourceCompatibility = '17'
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.kafka:spring-kafka'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testImplementation 'org.springframework.kafka:spring-kafka-test'
}

tasks.named('test') {
	useJUnitPlatform()
}
```
`KafkaProducerApplication.java`
````java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class KafkaProducerApplication {

	public static void main(String[] args) {
		SpringApplication.run(KafkaProducerApplication.class, args);
	}

}
````
`KafkaConfig.java`
```java
import org.apache.kafka.clients.admin.AdminClient;
import org.apache.kafka.clients.admin.AdminClientConfig;
import org.apache.kafka.clients.admin.NewTopic;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.core.KafkaAdmin;

import java.util.HashMap;
import java.util.Map;

@Configuration
public class KafkaConfig {

    private final String bootstrapAddress = "localhost:9092";

    @Bean
    public KafkaAdmin kafkaAdmin() {
        Map<String, Object> configs = new HashMap<>();
        configs.put(AdminClientConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapAddress);
        return new KafkaAdmin(configs);
    }

    @Bean
    public AdminClient adminClient() {
        return AdminClient.create(kafkaAdmin().getConfigurationProperties());
    }

    @Bean
    public NewTopic topic() {
        return new NewTopic("example-topic", 3, (short) 1);
    }
}
```
`KafkaProducerService.java`
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Service;

@Service
public class KafkaProducerService {

    private final KafkaTemplate<String, String> kafkaTemplate;
    private final String topicName = "example-topic";

    @Autowired
    public KafkaProducerService(KafkaTemplate<String, String> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public void sendMessage(String message, int partition) {
        kafkaTemplate.send(topicName, partition, null, message);
        System.out.println("Published message: " + message + " to partition: " + partition);
    }

    public void sendMessage(String key, int partition, String message) {
        kafkaTemplate.send(topicName, partition, key, message);
        System.out.println("Published message: " + message + " to partition: " + partition +" key: "+key);
    }
}
```
`KafkaProducerController.java`
```java
import com.example.kafka.producer.KafkaProducerService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class KafkaProducerController {

    private final KafkaProducerService kafkaProducerService;

    @Autowired
    public KafkaProducerController(KafkaProducerService kafkaProducerService) {
        this.kafkaProducerService = kafkaProducerService;
    }

    @PostMapping("/publish")
    public void publishMessage(@RequestBody String message, @RequestParam(defaultValue = "0") int partition) {
        kafkaProducerService.sendMessage(message, partition);
    }

    @PostMapping("/publish-key")
    public void publishMessage1(@RequestParam String key, @RequestParam(defaultValue = "0") int partition,
                                @RequestBody String message) {
        kafkaProducerService.sendMessage(key, partition ,message);
    }
}
```
### Example in Spring Reactor 
`pom.xml`
```xml
<dependencies>
    <!-- Spring Boot Starter -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>

    <!-- Spring Kafka -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-kafka</artifactId>
    </dependency>

    <!-- Reactor Kafka -->
    <dependency>
        <groupId>io.projectreactor.kafka</groupId>
        <artifactId>reactor-kafka</artifactId>
    </dependency>
</dependencies>
```
`KafkaProducerService.java`
```java
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.clients.producer.RecordMetadata;
import org.apache.kafka.common.serialization.StringSerializer;
import org.springframework.kafka.core.DefaultKafkaProducerFactory;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.kafka.support.KafkaHeaders;
import org.springframework.kafka.support.SendResult;
import org.springframework.messaging.support.GenericMessage;
import org.springframework.stereotype.Service;
import org.springframework.util.concurrent.ListenableFuture;
import reactor.core.publisher.Mono;
import reactor.core.publisher.MonoSink;

import javax.annotation.PostConstruct;
import java.util.HashMap;
import java.util.Map;

@Service
public class KafkaProducerService {

    private final KafkaTemplate<String, String> kafkaTemplate;

    public KafkaProducerService(KafkaTemplate<String, String> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public Mono<RecordMetadata> sendMessage(String topic, String key, String value) {
        ProducerRecord<String, String> record = new ProducerRecord<>(topic, key, value);
        GenericMessage<ProducerRecord<String, String>> message = new GenericMessage<>(record);
        message.getHeaders().add(KafkaHeaders.MESSAGE_KEY, key);

        return Mono.create(sink -> {
            ListenableFuture<SendResult<String, String>> future = kafkaTemplate.send(message);
            future.addCallback(result -> {
                RecordMetadata metadata = result.getRecordMetadata();
                sink.success(metadata);
            }, ex -> sink.error(ex));
        });
    }

    @PostConstruct
    private void configureSerializer() {
        Map<String, Object> configs = new HashMap<>();
        configs.put("key.serializer", StringSerializer.class);
        configs.put("value.serializer", StringSerializer.class);
        ((DefaultKafkaProducerFactory<?, ?>) kafkaTemplate.getProducerFactory()).setConfigurationProperties(configs);
    }
}
```
In this example, we define a `KafkaProducerService` class that handles sending messages to Kafka. The `sendMessage` method takes a `topic`, `key`, and `value`, and creates a `ProducerRecord` and a `GenericMessage` similar to the previous example.

We use `Mono.create` to create a custom `Mono`, which allows us to bridge between the reactive and callback-based world. Inside this custom `Mono`, we use `kafkaTemplate.send` to send the message asynchronously. We add a success and error callback to handle the result of the send operation. If successful, we retrieve the `RecordMetadata` and call `sink.success(metadata)` to emit it. If there's an error, we call `sink.error(ex)` to emit the error.

The `@PostConstruct` method `configureSerializer` sets the serializer properties for the Kafka producer factory used by the `KafkaTemplate`. In this example, we're using `StringSerializer` for both the key and value serializers.

`KafkaProducerController.java`
```java
import org.apache.kafka.clients.producer.RecordMetadata;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class KafkaProducerController {

    private final KafkaProducerService producerService;

    public KafkaProducerController(KafkaProducerService producerService) {
        this.producerService = producerService;
    }

    @PostMapping("/messages")
    public Mono<RecordMetadata> sendMessage(@RequestBody MessageRequest request) {
        return producerService.sendMessage(request.getTopic(), request.getKey(), request.getValue());
    }
}
```
`MessageRequest.java`
```java
public class MessageRequest {

    private String topic;
    private String key;
    private String value;

    // Getters and setters

    // Constructors
}
```
