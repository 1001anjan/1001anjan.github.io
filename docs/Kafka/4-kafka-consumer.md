---
layout: default
title: Kafka Consumer
parent: Kafka
nav_order: 4
---
### Kafka consumer using Spring Kafka(Listener based):
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
</dependencies>
```
`KafkaConsumerConfig.java`
```java
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.common.serialization.StringDeserializer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.annotation.EnableKafka;
import org.springframework.kafka.config.ConcurrentKafkaListenerContainerFactory;
import org.springframework.kafka.core.DefaultKafkaConsumerFactory;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.kafka.core.consumer.KafkaConsumerFactory;

import java.util.HashMap;
import java.util.Map;

@Configuration
@EnableKafka
public class KafkaConsumerConfig {

    private final String bootstrapServers = "localhost:9092";
    private final String groupId = "my-consumer-group";

    @Bean
    public Map<String, Object> consumerConfigs() {
        Map<String, Object> props = new HashMap<>();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
        props.put(ConsumerConfig.GROUP_ID_CONFIG, groupId);
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        return props;
    }

    @Bean
    public KafkaConsumerFactory<String, String> consumerFactory() {
        return new DefaultKafkaConsumerFactory<>(consumerConfigs());
    }

    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, String> kafkaListenerContainerFactory() {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(consumerFactory());
        return factory;
    }

    @Bean
    public KafkaTemplate<String, String> kafkaTemplate() {
        return new KafkaTemplate<>(consumerFactory());
    }
}
```
`KafkaConsumerService.java`
```java
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Service;

@Service
public class KafkaConsumerService {

    @KafkaListener(topics = "my-topic")
    public void consumeMessage(String message) {
        System.out.println("Received message: " + message);
        // Process the received message
    }
}
```
In this example, we define a `KafkaConsumerService` class that handles consuming messages from Kafka. We use the `@KafkaListener` annotation to specify the topic(s) to listen to. In this case, we listen to the `"my-topic"` topic.

The `consumeMessage` method is the actual message consumer. It takes the received message as a parameter and performs any necessary processing. In this example, we simply print the received message to the console, but you can implement your own business logic.

`SpringBootKafkaConsumerApplication.java`
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootKafkaConsumerApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBootKafkaConsumerApplication.class, args);
    }
}
```

### Kafka Consumer using poll based
`KafkaConsumer.java`
```java
import org.apache.kafka.clients.consumer.Consumer;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.common.serialization.StringDeserializer;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
import java.time.Duration;
import java.util.Collections;
import java.util.Properties;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

@Component
public class KafkaConsumer {

    @Value("${kafka.bootstrap.servers}")
    private String bootstrapServers;

    @Value("${kafka.consumer.group-id}")
    private String groupId;

    @Value("${kafka.topic}")
    private String topic;

    private ExecutorService executorService;
    private Consumer<String, Object> consumer;

    @PostConstruct
    public void initialize() {
        executorService = Executors.newFixedThreadPool(10);
        consumer = createConsumer();
        consumer.subscribe(Collections.singletonList(topic));

        executorService.submit(this::consumeMessages);
    }

    @PreDestroy
    public void shutdown() {
        consumer.wakeup();
        executorService.shutdown();
    }

    private Consumer<String, Object> createConsumer() {
        Properties props = new Properties();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.GROUP_ID_CONFIG, groupId);
        return new KafkaConsumer<>(props);
    }

    private void consumeMessages() {
        try {
            while (true) {
                ConsumerRecords<String, Object> records = consumer.poll(Duration.ofMillis(100));
                for (ConsumerRecord<String, Object> record : records) {
                    executorService.submit(() -> {
                        // Process the consumed message
                        String key = record.key();
                        Object value = record.value();
                        System.out.println("Received message: key = " + key + ", value = " + value);
                    });
                }
            }
        } catch (Exception e) {
            // Handle exception
        } finally {
            consumer.close();
        }
    }
}
```
In this updated version, the `@KafkaListener` annotation is removed, and the `consumer.poll()` method is used to poll for new messages. The `initialize()` method is annotated with `@PostConstruct`, which ensures that it is called after the bean is constructed. Inside this method, the Kafka consumer is created, subscribed to the topic, and a separate thread is started to consume messages using `consumer.poll()`.

The `shutdown()` method, annotated with `@PreDestroy`, is called when the application is shutting down. It triggers the `consumer.wakeup()` method to interrupt the `poll()` loop and gracefully shutdown the consumer and executor service.

### Kafka consumer wakeup method
The wakeup method is used in Apache Kafka Consumer API to interrupt the consumer's fetch loop and cause it to throw a `WakeupException`. This can be useful in situations where you want to shut down a consumer gracefully, without waiting for the poll loop to complete.

For example, you may have a scenario where you want to stop consuming messages from a topic and perform some cleanup actions. You can call the wakeup method on the consumer instance in another thread, which will interrupt the poll method and allow you to perform your cleanup logic before closing the consumer.

Here's an example implementation:

```java
class KafkaConsumerRunner {
    private final Consumer<String, String> consumer;
    private volatile boolean shutdown = false;

    public void runConsumer() {
        try {
            while (!shutdown) {
                ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
                // process the records
            }
        } catch (WakeupException e) {
            if (!shutdown) {
                throw e;
            }
        } finally {
            consumer.close();
        }
    }

    public void shutdown() {
        shutdown = true;
        consumer.wakeup();
    }
}
```

In this example, the runConsumer method polls for messages from a Kafka topic and processes them. The shutdown method sets the shutdown flag to true and calls wakeup on the consumer instance, which will interrupt the poll method and allow for clean shutdown of the consumer.

`consumerThreadPool.shutdown()` is used to stop the execution of tasks in a thread pool. It stops accepting new tasks, but waits for the running tasks to complete. When all running tasks are completed, the thread pool is considered shut down.

In your case, you would use this method to stop the thread pool that is executing the consumer's polling loop. After that, you would call `consumer.wakeup()` to interrupt the polling loop and trigger a `WakeupException`, allowing you to perform any necessary cleanup logic before closing the consumer.

Here's an example implementation:

```java
class KafkaConsumerRunner{
    private final ExecutorService consumerThreadPool;
    private final Consumer<String, String> consumer;
    private volatile boolean shutdown = false;

    public void runConsumer() {
        try {
            while (!shutdown) {
                ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
                // process the records
            }
        } catch (WakeupException e) {
            if (!shutdown) {
                throw e;
            }
        } finally {
            consumer.close();
        }
    }

    public void shutdown() {
        shutdown = true;
        consumer.wakeup();
        consumerThreadPool.shutdown();
    }
}

```
In this example, the shutdown method sets the shutdown flag to true and calls `consumerThreadPool.shutdown()` to stop the consumer's thread pool, and then calls `consumer.wakeup()` to interrupt the poll method and trigger a `WakeupException`. This allows you to perform any necessary cleanup logic before closing the consumer.

### Implement multiple listener

In Spring Boot, you can implement multiple listeners for Kafka by creating multiple methods and annotating them with `@KafkaListener`. Each method should have a unique topic and group id. For example:

```java
@KafkaListener(topics = "topic1", groupId = "group1")
public void listenTopic1(String message) {
    // handle message for topic1
}

@KafkaListener(topics = "topic2", groupId = "group2")
public void listenTopic2(String message) {
    // handle message for topic2
}
```
You can also configure multiple listeners by creating multiple Kafka listener container factories and configuring them with different group ids and concurrency.

```java
@Bean
public KafkaListenerContainerFactory<ConcurrentMessageListenerContainer<String, String>> 
  kafkaListenerContainerFactory1() {
    ConcurrentKafkaListenerContainerFactory<String, String> factory =
        new ConcurrentKafkaListenerContainerFactory<>();
    factory.setConsumerFactory(consumerFactory());
    factory.setConcurrency(3);
    factory.getContainerProperties().setPollTimeout(3000);
    return factory;
}
```
You can then annotate your listener methods with the appropriate container factory bean.

```java
@KafkaListener(topics = "topic1", containerFactory = "kafkaListenerContainerFactory1")
public void listenTopic1(String message) {
    // handle message for topic1
}
```
Here's a sample example in Spring Boot to implement multiple listeners for Kafka:

```java
@SpringBootApplication
public class KafkaMultipleListenersExample {

    @Value("${kafka.bootstrap-servers}")
    private String bootstrapServers;

    public static void main(String[] args) {
        SpringApplication.run(KafkaMultipleListenersExample.class, args);
    }

    @Bean
    public Map<String, Object> consumerConfigs() {
        Map<String, Object> props = new HashMap<>();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        return props;
    }

    @Bean
    public ConsumerFactory<String, String> consumerFactory() {
        return new DefaultKafkaConsumerFactory<>(consumerConfigs());
    }

    @Bean
    public KafkaListenerContainerFactory<ConcurrentMessageListenerContainer<String, String>> kafkaListenerContainerFactory1() {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(consumerFactory());
        factory.setConcurrency(3);
        return factory;
    }

    @Bean
    public KafkaListenerContainerFactory<ConcurrentMessageListenerContainer<String, String>> kafkaListenerContainerFactory2() {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(consumerFactory());
        factory.setConcurrency(2);
        return factory;
    }

    @KafkaListener(topics = "topic1", containerFactory = "kafkaListenerContainerFactory1")
    public void listenTopic1(String message) {
        System.out.println("Received message from topic1: " + message);
    }

    @KafkaListener(topics = "topic2", containerFactory = "kafkaListenerContainerFactory2")
    public void listenTopic2(String message) {
        System.out.println("Received message from topic2: " + message);
    }
}
```
In this example, we have two listener methods `listenTopic1` and `listenTopic2` each for a different topic. Each of these methods is annotated with `@KafkaListener` and configured to use a different Kafka listener container factory `kafkaListenerContainerFactory1` and `kafkaListenerContainerFactory2` respectively. These container factories are created and configured using the `kafkaListenerContainerFactory1` and `kafkaListenerContainerFactory2` methods.

In Spring Boot, the Kafka consumer is automatically managed by the framework, so you do not need to explicitly shut it down when the application stops.

When the application context is closed, for example, when the application is shut down or restarted, the consumer is automatically closed and all its resources are cleaned up.

However, if you need to manually shut down the consumer in a controlled manner, you can use the `KafkaListenerEndpointRegistry` to get a reference to the listener container and stop it.

Here's an example:

```java
@Autowired
private KafkaListenerEndpointRegistry kafkaListenerEndpointRegistry;

...

@PreDestroy
public void stopKafkaConsumer() {
    kafkaListenerEndpointRegistry.stop();
}
```
In this example, the `stopKafkaConsumer` method annotated with `@PreDestroy` is called when the application is shut down, and it stops the Kafka consumer using the `KafkaListenerEndpointRegistry`.

### Difference between kafka poll and  kafka listener
The difference between using the Kafka consumer poll method and the Kafka listener in Spring Boot is in the way that messages are consumed from a Kafka topic.

### Kafka Consumer Poll: 
The poll method is a low-level API that allows you to manually poll for messages from a Kafka topic. You have to manage the consumer offsets and handle the consumer rebalance events yourself. You also have to handle threading, batching, and error handling yourself.
Example:

```scala
public void pollKafka() {
    Consumer<String, String> consumer = createConsumer();

    while (true) {
        ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
        for (ConsumerRecord<String, String> record : records) {
            System.out.println("Received message: " + record.value());
        }
    }
}

```
### Kafka Listener: 
The Kafka listener in Spring Boot provides a higher-level abstraction on top of the poll method. The listener automatically manages the consumer offsets and handles the consumer rebalance events for you. The framework also provides built-in support for batch processing, error handling, and concurrency control.
Example:
```scala
@KafkaListener(topics = "topic")
public void listen(String message) {
    System.out.println("Received message: " + message);
}
```
In general, the Kafka listener is easier to use and provides more features compared to the poll method, making it the preferred choice for most use cases in a Spring Boot application.

#### Note1
The poll mechanism in Kafka is a low-level API that allows you to manually poll for messages from a Kafka topic. You have to manage the consumer offsets, handle the consumer rebalance events, handle threading, batching, and error handling yourself.

Here are some use cases where using the poll mechanism might be appropriate:

1. Custom processing logic: When you need to implement custom processing logic that is not supported by the Kafka listener, you might choose to use the poll mechanism. For example, if you need to process messages in a specific order, you might use the poll method to implement the custom logic.
2. Real-time streaming: When you need to process messages in real-time, you might choose to use the poll mechanism. This allows you to have full control over the polling frequency and the processing of messages.
3. Legacy applications: If you have an existing application that uses the poll mechanism, you might continue to use it instead of switching to the Kafka listener.
4. Performance optimization: If you have specific performance requirements and need to fine-tune the polling frequency and batch size, you might choose to use the poll mechanism.

In general, the poll mechanism is more complex and requires more manual work compared to the Kafka listener, but it offers more control and flexibility over the consumption of messages from a Kafka topic

#### Note 2
Spring Framework managed Kafka listener is best suited for simple to moderate data processing and can handle the load with its automatic partition assignment and offset management.

On the other hand, the Kafka Consumer API with manual poll approach provides more control and customization over the consumption process, making it suitable for more complex and large scale data processing scenarios.

Ultimately, the choice between these two approaches should be based on the specific requirements of your use case and the trade-off between ease of use and customization.

## How to avoid multiple consumers consuming the same message
To avoid multiple consumers consuming the same message, you can make use of partitions in Apache Kafka. Each topic in Kafka is divided into one or more partitions, and each message within a partition is assigned a unique offset.

By default, Kafka assigns messages to partitions in a round-robin fashion, ensuring that each partition is consumed by only one consumer within a consumer group. This ensures that multiple consumers within the same group don't process the same message.

To implement this in your Spring Boot application, you need to configure the number of partitions for the topic and set the `group.id` property appropriately. 

Here's an updated example:
`KafkaConsumerConfig.java`
```java
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.common.serialization.StringDeserializer;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.config.ConcurrentKafkaListenerContainerFactory;
import org.springframework.kafka.core.DefaultKafkaConsumerFactory;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.kafka.core.consumer.KafkaConsumerFactory;

import java.util.HashMap;
import java.util.Map;

@Configuration
public class KafkaConsumerConfig {
    @Value("${spring.kafka.bootstrap-servers}")
    private String bootstrapServers;

    @Value("${spring.kafka.consumer.group-id}")
    private String groupId;

    @Value("${spring.kafka.consumer.concurrency}")
    private int concurrency;

    @Bean
    public Map<String, Object> consumerConfigs() {
        Map<String, Object> props = new HashMap<>();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        props.put(ConsumerConfig.GROUP_ID_CONFIG, groupId);
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 1); // Ensures each consumer gets only one record per poll
        return props;
    }

    @Bean
    public KafkaConsumerFactory<String, String> consumerFactory() {
        return new DefaultKafkaConsumerFactory<>(consumerConfigs());
    }

    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, String> kafkaListenerContainerFactory() {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(consumerFactory());
        factory.setConcurrency(concurrency);
        factory.getContainerProperties().setPollTimeout(3000); // Adjust the poll timeout as per your needs
        return factory;
    }
}
```
In the above code, we've added a new property `concurrency` which represents the number of consumer instances within the same consumer group. This allows multiple consumers to process messages concurrently.

`KafkaConsumer.java`
```java
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Component;

@Component
public class KafkaConsumer {
    @KafkaListener(topics = "my-topic", groupId = "my-group")
    public void consume(String message) {
        // Process the received message
        System.out.println("Received message: " + message);
    }
}
```
Ensure that you have created the topic with multiple partitions before running the application. You can do this using the Kafka command-line tools or programmatically using the Kafka Admin Client in your application.

By configuring the appropriate number of partitions and consumer group, Kafka ensures that each message within a partition is consumed by only one consumer instance at a time. This way, you can avoid multiple consumers consuming the same message.

Note: If you need strict ordering of messages, where each message is processed in the order it is received, you should use a single partition for the topic. Using multiple partitions allows for parallel processing but may not guarantee strict message ordering across partitions.

### consumer `group.id `
The consumer `group.id` in Apache Kafka is a property that identifies a group of consumers that work together to consume messages from one or more topics. Kafka uses this property to manage the distribution of messages across the consumers within the group.

When multiple consumers belong to the same consumer group and subscribe to the same topic, Kafka ensures that each message is delivered to only one consumer within the group. This ensures load balancing and allows for parallel processing of messages.

The `group.id` serves as an identifier for the consumer group and helps Kafka keep track of the progress of each consumer within the group. Kafka maintains the offset for each consumer, which represents the position of the last consumed message within each partition. By tracking the offsets, Kafka ensures that each consumer within the group continues from where it left off in case of failures or restarts.

Here are some key points about the `group.id` property:
1. Consumers with the same `group.id` belong to the same consumer group.
2. Each partition within a topic is consumed by only one consumer within the group at a time.
3. Kafka automatically balances the partitions across consumers in the group, ensuring that each consumer gets a roughly equal number of partitions to process.
4. If a consumer within the group fails or leaves the group, Kafka automatically reassigns its partitions to other active consumers in the group.
5. Each consumer group maintains its own set of offsets, allowing consumers to work independently and process messages at their own pace.

By setting different `group.id` values for different consumer groups, you can have multiple independent groups consuming messages from the same or different topics. This allows for scalability and flexibility in distributing the workload across multiple consumer instances.




