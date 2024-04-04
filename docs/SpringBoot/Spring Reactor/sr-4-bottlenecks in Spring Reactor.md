---
layout: default
title: Bottlenecks in Spring Reactor
parent: Spring Reactor
grand_parent: Spring Boot
nav_order: 4
---
# Bottlenecks in Spring Reactor
There are several ways to handle bottlenecks in Spring Reactor:

1. Parallel Processing: Use the `parallel` operator to divide the stream into multiple parallel streams and process elements in parallel. This can help distribute the load and reduce the time taken to process elements.

2. Batching: Use the `buffer` operator to group elements into batches and process them in bulk. This can help reduce the overhead of processing individual elements and improve performance.

3. Backpressure: Use the `onBackpressureBuffer` or `onBackpressureDrop` operators to handle cases where the rate of incoming elements exceeds the rate of processing. The `onBackpressureBuffer` operator buffers incoming elements until they can be processed, while the `onBackpressureDrop` operator drops elements if the rate of incoming elements exceeds the rate of processing.

4. Scheduling: Use the `subscribeOn` operator to specify the scheduler that should be used to process elements. You can use a different scheduler for different stages of the stream to ensure that the processing can be optimized based on the requirements of each stage.

5. Caching: Use the `cache` operator to cache the results of a reactive stream. This can help reduce the overhead of processing elements that have already been processed, and improve performance.

In addition to these strategies, it's also important to monitor the performance of your reactive streams and adjust the configuration of your application to ensure that it can handle the load. This may involve adjusting the number of threads, adjusting the buffer sizes, or adjusting the configuration of your schedulers.

### Here's an example of using parallel processing, batching, and scheduling in a Spring Boot application to handle a bottleneck scenario:
```java
@RestController
public class ExampleController {

  private final ReactiveMongoTemplate template;

  public ExampleController(ReactiveMongoTemplate template) {
    this.template = template;
  }

  @GetMapping("/data/parallel")
  public Flux<Data> getDataParallel() {
    return template.find(Query.empty(), Data.class)
      .parallel(8)
      .runOn(Schedulers.parallel())
      .buffer(1024)
      .flatMap(dataList -> {
        // Do some processing on dataList
        return Flux.fromIterable(dataList);
      });
  }
}
```
In this example, the controller has an endpoint `/data/parallel` that returns a reactive stream of Data objects.

The reactive stream is created using the `template.find` method to fetch data from a `MongoDB` database. The `parallel` operator is used to divide the stream into 8 parallel streams to process elements in parallel. The `runOn` operator is used to specify the `Schedulers.parallel` scheduler, which is optimized for parallel processing.

The `buffer` operator is used to group elements into batches of 1024, so that elements can be processed in bulk. Finally, the `flatMap` operator is used to do some processing on each batch of elements, and return the processed elements as a reactive stream.

By using parallel processing, batching, and scheduling, this code can handle a bottleneck scenario by distributing the load, reducing the overhead of processing elements, and optimizing the processing of elements based on the requirements of each stage.

### Here's an example of using the `onBackpressureBuffer` operator to handle backpressure in a Spring Boot application:

```java
@RestController
public class ExampleController {

  private final Flux<Integer> hotFlux;

  public ExampleController() {
    this.hotFlux = Flux.create(sink -> {
      for (int i = 0; i < 10000; i++) {
        sink.next(i);
      }
      sink.complete();
    });
  }

  @GetMapping("/data")
  public Flux<Integer> getData() {
    return hotFlux.onBackpressureBuffer(1024);
  }
}
```
In this example, the controller has an endpoint `/data` that returns a reactive stream of integers. The `hotFlux` is created using the `Flux.create` method, and it generates a stream of 10,000 integers.

The `onBackpressureBuffer` operator is used to handle cases where the rate of incoming elements exceeds the rate of processing. In this example, the buffer size is set to 1024, so that incoming elements are buffered until they can be processed.

By using the `onBackpressureBuffer` operator, this code can handle a backpressure scenario by buffering incoming elements and ensuring that the reactive stream can continue to process elements even if the rate of incoming elements exceeds the rate of processing.

### Here's an example of using the `onBackpressureDrop` operator to handle backpressure in a Spring Boot application:

```java
@RestController
public class ExampleController {

  private final Flux<Integer> hotFlux;

  public ExampleController() {
    this.hotFlux = Flux.create(sink -> {
      for (int i = 0; i < 10000; i++) {
        sink.next(i);
      }
      sink.complete();
    });
  }

  @GetMapping("/data")
  public Flux<Integer> getData() {
    return hotFlux.onBackpressureDrop(i -> {
      // Log dropped element
      System.out.println("Dropped element: " + i);
    });
  }
}
```

In this example, the controller has an endpoint `/data` that returns a reactive stream of integers. The `hotFlux` is created using the `Flux.create` method, and it generates a stream of 10,000 integers.

The `onBackpressureDrop` operator is used to handle cases where the rate of incoming elements exceeds the rate of processing. In this example, the operator is configured to drop incoming elements and log a message for each dropped element.

By using the `onBackpressureDrop operator`, this code can handle a backpressure scenario by dropping incoming elements and ensuring that the reactive stream can continue to process elements even if the rate of incoming elements exceeds the rate of processing.

### A scheduler in Spring Reactor
A `scheduler` in Spring Reactor is a component that is responsible for executing tasks asynchronously. It provides a mechanism for scheduling the execution of reactive streams and other tasks, such as timer-based operations, event handling, and task scheduling.

Schedulers in Spring Reactor can be used to control the concurrency and parallelism of reactive streams, as well as to perform other operations such as error handling, backpressure handling, and resource management.

The Scheduler interface in Spring Reactor provides methods for scheduling the execution of tasks, such as `schedule`, `schedulePeriodically`, and `dispose`. There are also several built-in scheduler implementations in Spring Reactor, such as the `Schedulers.boundedElastic` and `Schedulers.parallel` schedulers.

When creating a reactive stream in Spring Reactor, you can specify which scheduler to use for executing tasks. This allows you to control the concurrency and parallelism of the stream, and to ensure that tasks are executed in the correct order.

For example, you can use the `subscribeOn` operator to specify the scheduler to use for executing a stream:

```java
Flux.just(1, 2, 3)
  .subscribeOn(Schedulers.boundedElastic())
  .subscribe(System.out::println);
```

In this example, the `subscribeOn` operator is used to specify that the stream should be executed on the `Schedulers.boundedElastic` scheduler.

### Compare `Schedulers.boundedElastic` and `Schedulers.parallel`
`Schedulers.boundedElastic` and `Schedulers.parallel` are two different scheduler implementations in Spring Reactor.

`Schedulers.boundedElastic` is a scheduler that creates a new thread for each task and is suitable for IO-bound and non-blocking tasks. It uses a dynamic pool of threads that can grow or shrink based on the rate of incoming tasks. This scheduler is useful for scenarios where the rate of incoming tasks can vary dynamically, as it can adapt to the changing load.

Schedulers.parallel is a scheduler that uses a fixed-size pool of threads to execute tasks in parallel. It is suitable for CPU-bound tasks that require a large number of threads to achieve maximum performance. This scheduler is useful for scenarios where the rate of incoming tasks is known in advance and is constant, as it provides predictable performance.

In general, `Schedulers.boundedElastic` is a good choice for IO-bound tasks, while `Schedulers.parallel` is a good choice for CPU-bound tasks. However, the choice of scheduler ultimately depends on the specific requirements of your application and the nature of the tasks you need to perform.

You can use the subscribeOn operator in Spring Reactor to specify which scheduler to use for executing a reactive stream. For example:

```java
Flux.just(1, 2, 3)
  .subscribeOn(Schedulers.boundedElastic())
  .subscribe(System.out::println);
```

In this example, the `subscribeOn` operator is used to specify that the stream should be executed on the `Schedulers.boundedElastic` scheduler.

### Here is an example of how you can send a `202 Accepted` response in a Spring Boot application while executing a task in the background:

Here is an example of how you can send a response immediately in a Spring Boot application while executing a task in the background:
```java
@RestController
public class ExampleController {

  @GetMapping("/background-task")
  public Mono<String> executeBackgroundTask() {
    return Mono.fromCallable(() -> {
      // Simulate a long-running task
      try {
        Thread.sleep(5000);
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
      return "Task completed";
    }).subscribeOn(Schedulers.elastic())
      .doOnSubscribe(subscription -> {
        // Send immediate response to client
        return Mono.just("Task started").subscribe(System.out::println);
      });
  }
}
```

In this example, the endpoint /`background-task` returns a reactive stream represented by the `Mono` class. The `fromCallable` method is used to create a Mono that executes a callable task, in this case a long-running task that simulates a delay of 5 seconds.

The `subscribeOn` operator is used to specify that the task should be executed on the `Schedulers.elastic` scheduler, which is a scheduler that creates a new thread for each task and is suitable for IO-bound and non-blocking tasks.

The `doOnSubscribe` operator is used to specify an action that should be performed when a client subscribes to the stream. In this case, the action sends an immediate response to the client with the message `"Task started"`.

To test this example, you can send a request to the `/background-task` endpoint and observe that the response is sent immediately, while the task is executed in the background.

### Here is an example of how you can send a `202 Accepted` response in a Spring Boot application while executing a task in the background:

```java
@RestController
public class ExampleController {

  @GetMapping("/background-task")
  public Mono<Void> executeBackgroundTask() {
    return Mono.fromRunnable(() -> {
      // Simulate a long-running task
      try {
        Thread.sleep(5000);
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }).subscribeOn(Schedulers.elastic())
      .doOnSubscribe(subscription -> {
        // Send immediate response to client
        return ServerResponse.accepted().build().subscribe();
      });
  }
}
```

In this example, the endpoint `/background-task` returns a reactive stream represented by the `Mono` class. The `fromRunnable` method is used to create a `Mono` that executes a runnable task, in this case a long-running task that simulates a delay of 5 seconds.

The `subscribeOn` operator is used to specify that the task should be executed on the `Schedulers.elastic` scheduler, which is a scheduler that creates a new thread for each task and is suitable for IO-bound and non-blocking tasks.

The `doOnSubscribe` operator is used to specify an action that should be performed when a client subscribes to the stream. In this case, the action sends an immediate `202 Accepted` response to the client. This is done by creating a `ServerResponse` object with the accepted method and then calling the build method to build the response. The `subscribe` method is then called to send the response.

To test this example, you can send a request to the `/background-task` endpoint and observe that the response is sent immediately with the `202 Accepted` status code, while the task is executed in the background.

### Compare `Schedulers.elastic` and `Schedulers.boundedElastic`
`Schedulers.elastic()` and `Schedulers.boundedElastic()` are both schedulers provided by Spring Reactor that can be used to execute tasks asynchronously. However, they have some differences:

1. Thread Pool Size: `Schedulers.elastic()` creates a new thread for each task, while `Schedulers.boundedElastic()` uses a bounded thread pool with a fixed number of threads.

2. Resource utilization: `Schedulers.elastic()` can potentially consume a large amount of resources if there are many tasks, as it creates a new thread for each task. On the other hand, `Schedulers.boundedElastic()` has a fixed number of threads and will queue tasks if all threads are busy, making it more suitable for use-cases where the number of tasks is expected to be large.

3. Performance: `Schedulers.elastic()` has lower overhead compared to `Schedulers.boundedElastic()`, as it does not need to manage a thread pool. However, it can potentially slow down other tasks if there are too many tasks running concurrently. `Schedulers.boundedElastic()` may have higher overhead, but it can provide better performance by managing the number of tasks and ensuring that they are executed in a timely manner.

In general, you should choose `Schedulers.elastic()` if you have a small number of tasks or if you want to minimize overhead, and `Schedulers.boundedElastic()` if you have a large number of tasks or if you need to ensure that tasks are executed in a timely manner.

### Note:
To configure the pool size for `Schedulers.boundedElastic()`, you can use the `.create()` method and specify the number of threads in the thread pool. Here's an example:

```java
Scheduler boundedElasticScheduler = Schedulers.boundedElastic()
                                              .create(10); // specify the number of threads in the pool
```
In this example, the thread pool size is set to 10, which means that at most 10 tasks can be executed concurrently. Any additional tasks will be queued until a thread becomes available.

### Compare `Mono.fromRunnable` and `Mono.fromCallable`:

`Mono.fromRunnable` and `Mono.fromCallable` are both factory methods in Spring Reactor that can be used to create a Mono from a `Runnable` and `Callable` respectively.

Here's a comparison between the two:

1. Return type: `Mono.fromRunnable` returns a `Mono<Void>`, meaning that it does not produce any value. On the other hand, `Mono.fromCallable` returns a `Mono<T>`, where `T` is the type of the value returned by the `Callable`.

2. Exception handling: `Mono.fromRunnable` does not allow for the capture of exceptions thrown by the `Runnable`. However, exceptions thrown by the `Callable` can be captured and returned as a `MonoError`.

3. Use case: `Mono.fromRunnable` is best suited for use-cases where you only need to run a side-effect and do not care about the result. `Mono.fromCallable` is best suited for use-cases where you need to perform a computation and return the result.

```java
@RestController
public class ExampleController {

    @GetMapping("/example")
    public Mono<String> example() {
        Callable<String> callable = () -> {
            if (Math.random() < 0.5) {
                throw new IllegalStateException("Random error");
            }
            return "Hello World";
        };

        return Mono.fromCallable(callable)
                   .onErrorResume(e -> Mono.just("Error Occurred"));
    }
}
```












