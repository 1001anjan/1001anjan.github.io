---
layout: default
title: implement multiple
parent: Quick Notes
grand_parent: Kafka
nav_order: 1
---
# Implement multiple

In Spring Boot, you can implement multiple listeners for Kafka by creating multiple methods and annotating them with @KafkaListener. Each method should have a unique topic and group id. For example:

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
In this example, we have two listener methods listenTopic1 and listenTopic2 each for a different topic. Each of these methods is annotated with @KafkaListener and configured to use a different Kafka listener container factory kafkaListenerContainerFactory1 and kafkaListenerContainerFactory2 respectively. These container factories are created and configured using the kafkaListenerContainerFactory1 and kafkaListenerContainerFactory2 methods.

In Spring Boot, the Kafka consumer is automatically managed by the framework, so you do not need to explicitly shut it down when the application stops.

When the application context is closed, for example, when the application is shut down or restarted, the consumer is automatically closed and all its resources are cleaned up.

However, if you need to manually shut down the consumer in a controlled manner, you can use the KafkaListenerEndpointRegistry to get a reference to the listener container and stop it.

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
In this example, the stopKafkaConsumer method annotated with @PreDestroy is called when the application is shut down, and it stops the Kafka consumer using the KafkaListenerEndpointRegistry.

### Difference between kafka poll and  kafka listener 
The difference between using the Kafka consumer poll method and the Kafka listener in Spring Boot is in the way that messages are consumed from a Kafka topic.

Kafka Consumer Poll: The poll method is a low-level API that allows you to manually poll for messages from a Kafka topic. You have to manage the consumer offsets and handle the consumer rebalance events yourself. You also have to handle threading, batching, and error handling yourself.
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
Kafka Listener: The Kafka listener in Spring Boot provides a higher-level abstraction on top of the poll method. The listener automatically manages the consumer offsets and handles the consumer rebalance events for you. The framework also provides built-in support for batch processing, error handling, and concurrency control.
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

Custom processing logic: When you need to implement custom processing logic that is not supported by the Kafka listener, you might choose to use the poll mechanism. For example, if you need to process messages in a specific order, you might use the poll method to implement the custom logic.

Real-time streaming: When you need to process messages in real-time, you might choose to use the poll mechanism. This allows you to have full control over the polling frequency and the processing of messages.

Legacy applications: If you have an existing application that uses the poll mechanism, you might continue to use it instead of switching to the Kafka listener.

Performance optimization: If you have specific performance requirements and need to fine-tune the polling frequency and batch size, you might choose to use the poll mechanism.

In general, the poll mechanism is more complex and requires more manual work compared to the Kafka listener, but it offers more control and flexibility over the consumption of messages from a Kafka topic

#### Note 2
Spring Framework managed Kafka listener is best suited for simple to moderate data processing and can handle the load with its automatic partition assignment and offset management.

On the other hand, the Kafka Consumer API with manual poll approach provides more control and customization over the consumption process, making it suitable for more complex and large scale data processing scenarios.

Ultimately, the choice between these two approaches should be based on the specific requirements of your use case and the trade-off between ease of use and customization.


