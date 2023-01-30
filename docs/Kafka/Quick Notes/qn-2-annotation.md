---
layout: default
title: Kafka consumer
parent: Quick Notes
grand_parent: Kafka
nav_order: 1
---
# Kafka consumer

### @PostConstruct
`@PostConstruct` is a JSR-250 annotation that indicates a method should be executed after the object has been instantiated and all dependencies have been injected. In other words, it is used to indicate a method that should be executed after the object is constructed and initialized. It is commonly used in Spring to execute any necessary initializations after the dependencies have been injected. The method annotated with @PostConstruct is guaranteed to be called only once in the life cycle of an object.

### @PreDestroy
`@PreDestroy` is a JSR-250 annotation that indicates a method should be executed before the object is destroyed by the container. It is commonly used in Spring to perform any necessary cleanup or resource release before the object is destroyed. The method annotated with @PreDestroy is guaranteed to be called only once in the life cycle of an object.

### Kafka consumer wakeup method
The wakeup method is used in Apache Kafka Consumer API to interrupt the consumer's fetch loop and cause it to throw a WakeupException. This can be useful in situations where you want to shut down a consumer gracefully, without waiting for the poll loop to complete.

For example, you may have a scenario where you want to stop consuming messages from a topic and perform some cleanup actions. You can call the wakeup method on the consumer instance in another thread, which will interrupt the poll method and allow you to perform your cleanup logic before closing the consumer.

Here's an example implementation:

```java
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
```

In this example, the runConsumer method polls for messages from a Kafka topic and processes them. The shutdown method sets the shutdown flag to true and calls wakeup on the consumer instance, which will interrupt the poll method and allow for clean shutdown of the consumer.

consumerThreadPool.shutdown() is used to stop the execution of tasks in a thread pool. It stops accepting new tasks, but waits for the running tasks to complete. When all running tasks are completed, the thread pool is considered shut down.

In your case, you would use this method to stop the thread pool that is executing the consumer's polling loop. After that, you would call consumer.wakeup() to interrupt the polling loop and trigger a WakeupException, allowing you to perform any necessary cleanup logic before closing the consumer.

Here's an example implementation:

```java
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

```
In this example, the shutdown method sets the shutdown flag to true and calls consumerThreadPool.shutdown() to stop the consumer's thread pool, and then calls consumer.wakeup() to interrupt the poll method and trigger a WakeupException. This allows you to perform any necessary cleanup logic before closing the consumer.

