---
layout: default
title: Reactor Operator II
parent: Spring Reactor
grand_parent: Spring Boot
nav_order: 3
---
# Reactor Operator II
Here is an example of using the `zipWith` operator in Spring Boot:

```java
@Service
public class OrderService {

    public Flux<Order> getOrders() {
        return Flux.just(
                new Order(1, "Order 1"),
                new Order(2, "Order 2"),
                new Order(3, "Order 3"),
                new Order(4, "Order 4")
        );
    }

    public Flux<OrderItem> getOrderItems(int orderId) {
        if (orderId == 1) {
            return Flux.just(
                    new OrderItem(1, "Item 1"),
                    new OrderItem(2, "Item 2"),
                    new OrderItem(3, "Item 3")
            );
        } else if (orderId == 2) {
            return Flux.just(
                    new OrderItem(4, "Item 4"),
                    new OrderItem(5, "Item 5")
            );
        } else if (orderId == 3) {
            return Flux.just(
                    new OrderItem(6, "Item 6"),
                    new OrderItem(7, "Item 7"),
                    new OrderItem(8, "Item 8"),
                    new OrderItem(9, "Item 9")
            );
        } else {
            return Flux.just(
                    new OrderItem(10, "Item 10"),
                    new OrderItem(11, "Item 11"),
                    new OrderItem(12, "Item 12")
            );
        }
    }
}

@RestController
public class OrderController {

    private final OrderService orderService;

    public OrderController(OrderService orderService) {
        this.orderService = orderService;
    }

    @GetMapping("/orders")
    public void getOrders() {
        orderService.getOrders()
                .flatMap(order -> orderService.getOrderItems(order.getId())
                        .collectList()
                        .map(orderItems -> {
                            order.setOrderItems(orderItems);
                            return order;
                        }))
                .subscribe(order -> {
                    System.out.println("Received order: " + order);
                }, error -> {
                    System.err.println("Error occured: " + error);
                }, () -> {
                    System.out.println("All orders received");
                });
    }
}
```
In this example, the `OrderService` returns a `Flux` of `Order` objects and has a method `getOrderItems` which returns a `Flux` of `OrderItem` objects for a given `orderId`. The `OrderController` then `flatmaps` the Order objects to fetch the corresponding `OrderItem` objects using the `getOrderItems` method. The `OrderItem` objects are then collected into a `List` and used to set the `OrderItem` list for the `Order` object. Finally, the updated `Order` objects are subscribed to and printed to the console. In case of an error, the error is printed to the error console. Finally, when all orders are received, a message is printed to the console indicating that all orders have been received.

### The `collectList` operator

The `collectList` operator in Spring Reactor can be used to gather the elements of a `Flux` or `Mono` into a single List. This operator can be useful when you need to gather all elements of a reactive stream into a single, non-reactive data structure, or when you need to pass a collection of elements to another method that only accepts a single argument.

It is important to note that the `collectList` operator will block the processing of the reactive stream until all elements have been emitted, so it should only be used in cases where it is acceptable for processing to wait for all elements to be available.

In general, you should use `collectList` when you need to collect all elements of a reactive stream into a single, non-reactive data structure for further processing, or when you need to pass a collection of elements to another method that only accepts a single argument.

### Here's an example in Spring Boot that demonstrates how to handle the elements of a `Flux` without using the `collectList` operator:

```java
@RestController
public class MyController {
  
  @GetMapping("/example")
  public Flux<String> example() {
    return Flux.just("A", "B", "C")
               .map(str -> "Element: " + str)
               .doOnNext(System.out::println);
  }
}
```
In this example, we are using a `Flux` to emit the elements "A", "B", and "C". We are then using the `map` operator to transform each element into a string with the format `"Element: X"`, where `X` is the original element. Finally, we are using the `doOnNext` operator to print each transformed element as it is emitted.

Without using `collectList`, this example demonstrates how to handle the elements of a reactive stream as they are emitted, without blocking processing or gathering all elements into a single data structure.

### The `reduce` operator

The `reduce` operator is a reactive programming operator used to aggregate the elements of a reactive stream into a single value. It works by applying a `BiFunction` to each element of the stream, starting with an initial value, and accumulating the result into a single value. The `BiFunction` takes two arguments: the accumulated value and the current element, and returns a new accumulated value. The final value is returned as a `Mono` or Single after all elements have been processed.

For example, if we have a `Flux` of integers, we can use the `reduce` operator to find the sum of all elements in the stream:

```java
Flux.just(1, 2, 3)
    .reduce(0, (sum, next) -> sum + next)
    .subscribe(sum -> System.out.println("Sum: " + sum));
```

This code would produce the output Sum: 6.

The `reduce` operator is useful for aggregating the elements of a reactive stream into a single value, such as summing numbers, concatenating strings, or finding the maximum or minimum value in a stream.

### Here's an example in Spring Boot that demonstrates how to use the `reduce` operator:

```java
@RestController
public class MyController {
  
  @GetMapping("/example")
  public Mono<String> example() {
    return Flux.just("A", "B", "C")
               .reduce("", (agg, next) -> agg + next)
               .map(str -> "Reduced string: " + str);
  }
}
```
In this example, we are using a `Flux` to emit the elements "A", "B", and "C". We are then using the `reduce` operator to concatenate all elements into a single string. The `reduce` operator takes two arguments: an initial value and a `BiFunction` that describes how to accumulate the elements. In this case, we are starting with an empty string "" and concatenating each element to the accumulated string.

Finally, we are using the `map` operator to transform the reduced string into a new string with the format `"Reduced string: X"`, where X is the reduced string.

This example demonstrates how to use the `reduce` operator to aggregate the elements of a reactive stream into a single value, in this case by concatenating the elements into a single string.

### The `doOnNext` operator

The `doOnNext` operator is a reactive programming operator used to perform an action for each element in a reactive stream before it is delivered to the `Subscriber`. It allows you to `side-effect` or modify the elements in the stream before they reach their final destination.

For example, you can use the `doOnNext` operator to log each element in a `Flux` before it is processed by the next operator or delivered to the subscriber:

```java
Flux.just(1, 2, 3)
    .doOnNext(element -> System.out.println("Element: " + element))
    .subscribe(System.out::println);
```
This code would produce the output:

```yaml
Element: 1
1
Element: 2
2
Element: 3
3
```

### Here's an example using the `doOnNext` operator in a Spring Boot application:
```java
@RestController
public class ExampleController {

    private final ReactiveUserRepository repository;

    public ExampleController(ReactiveUserRepository repository) {
        this.repository = repository;
    }

    @GetMapping("/users")
    public Mono<List<User>> getUsers() {
        return repository.findAll()
                        .doOnNext(user -> System.out.println("User fetched: " + user.getUsername()))
                        .collectList();
    }
}
```

In this example, we have a `RestController` that returns a `Mono` of a `List` of `User` objects, fetched from a reactive `UserRepository`. The `doOnNext` operator is used to log each `User` object as it is fetched from the repository. Finally, the collectList operator is used to collect all the elements in the stream into a single List.

Here's an example of how the `UserRepository` might be implemented:
```java
public interface ReactiveUserRepository extends ReactiveCrudRepository<User, Long> {
}
```

This `UserRepository` extends `ReactiveCrudRepository` from Spring Data, providing reactive CRUD operations for `User` objects.

### `doOnError` operator
`doOnError` is an operator in the Spring Reactor library that allows you to perform some action whenever an error occurs in the stream. The action can be any side-effect, such as logging, updating a database, or sending a notification.

For example, you can use the `doOnError` operator to log an error message when an exception occurs:

```java
Mono.error(new RuntimeException("Error occurred"))
    .doOnError(e -> System.out.println("Error: " + e.getMessage()))
    .subscribe();
```

In this example, a `Mono` with a runtime exception is created, and the `doOnError` operator is used to log the error message whenever an error occurs in the stream. The subscribe method is used to trigger the stream, which will result in the exception being thrown and the error message being logged.

Note that the `doOnError` operator does not prevent the error from propagating through the stream. It simply allows you to perform some action before the error is propagated to the next operator or to the subscribe method.

### Here is an example using the `doOnError` operator in a Spring Boot application:

Consider a scenario where we have an API endpoint that returns a `Mono` of a user's details, based on their username. If the user is not found, we want to log a warning message, and return an error response to the client.

Here's how you could implement this in Spring Boot:

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users/{username}")
    public Mono<ResponseEntity<User>> getUserDetails(@PathVariable String username) {
        return userService.getUserDetails(username)
            .doOnError(e -> log.warn("User not found: " + username))
            .map(user -> ResponseEntity.ok(user))
            .defaultIfEmpty(ResponseEntity.notFound().build());
    }
}
```
In this example, the `getUserDetails` method returns a `Mono` of a `ResponseEntity` that contains the user details. The `userService.getUserDetails(username)` method returns a `Mono` of a `User` object. If an error occurs (for example, if the user is not found), the `doOnError` operator is used to log a warning message.

Next, the `map` operator is used to convert the `User` object into a `ResponseEntity` with a `200 OK` status code. Finally, the `defaultIfEmpty` operator is used to return a `404 Not Found` response if the `Mono` is empty (i.e., if the user is not found).

### The `defaultIfEmpty` operator

The `defaultIfEmpty` operator is used to provide a default value if a reactive stream is empty. It means if the reactive stream doesn't emit any items, the `defaultIfEmpty` operator will emit a specified default value. This operator is useful in cases where we want to provide a default value when the reactive stream is empty. For example, in case of an empty database result, we can use this operator to emit a default value instead of an empty stream.

### `doOnErrorReturn` operator
`doOnErrorReturn` is an operator in the Reactor library of the Spring framework that allows you to specify a fallback value to be returned in case an error occurs during the processing of a reactive stream. It can be used to catch exceptions thrown during the processing of the reactive stream and instead of propagating the error, a specified fallback value can be returned. The operator takes as an argument a function that specifies the fallback value to be returned in case of an error. This operator is useful in scenarios where we want to handle specific exceptions and return a fallback value instead of propagating the error.

Here's a simple example of using the `doOnErrorReturn` operator in a Spring Boot application:

```java
@RestController
public class ExampleController {
  
  private final ReactiveMongoTemplate template;

  public ExampleController(ReactiveMongoTemplate template) {
    this.template = template;
  }

  @GetMapping("/data")
  public Mono<String> getData() {
    return template.findById("someId", Data.class)
      .map(Data::getValue)
      .doOnErrorReturn("Fallback value")
      .flatMap(value -> Mono.just("Processed value: " + value));
  }
}
```
In this example, the controller is fetching data from a `MongoDB` database using a `ReactiveMongoTemplate`. The findById method returns a `Mono` that emits the data. The map operator is used to extract the value field from the data. The `doOnErrorReturn` operator is used to specify a fallback value in case the `findById` method throws an error. Finally, the `flatMap` operator is used to process the value and return a `Mono` that emits the processed value as a string.

The `doOnErrorReturn` operator allows you to specify a fallback value that will be returned in case of an error, without having to manually handle the error in a catch block.

### The `doOnErrorResume` operator
The `doOnErrorResume` operator is a reactive programming operator that allows you to specify an alternative source to continue the processing of a reactive stream in case of an error. This operator takes a `Function` as an argument that maps the error to a new `Publisher` or `Mono` that will be used as a replacement for the original source. The new source will continue the emission of the reactive stream.

Here's a simple example of using the `doOnErrorResume` operator in a Spring Boot application:

```java
@RestController
public class ExampleController {
  
  private final ReactiveMongoTemplate template;

  public ExampleController(ReactiveMongoTemplate template) {
    this.template = template;
  }

  @GetMapping("/data")
  public Mono<String> getData() {
    return template.findById("someId", Data.class)
      .map(Data::getValue)
      .doOnErrorResume(error -> Mono.just("Fallback value"))
      .flatMap(value -> Mono.just("Processed value: " + value));
  }
}
```

In this example, the controller is fetching data from a `MongoDB` database using a `ReactiveMongoTemplate`. The `findById` method returns a `Mono` that emits the data. The `map` operator is used to extract the value field from the data. The `doOnErrorResume` operator is used to specify an alternative source in case the `findById` method throws an error. The `doOnErrorResume` operator takes a `Function` that maps the error to a new `Mono` that emits the fallback value. Finally, the `flatMap` operator is used to process the value and return a `Mono` that emits the processed value as a string.

The `doOnErrorResume` operator allows you to continue the processing of the reactive stream in case of an error by specifying a new source to replace the original source, which failed. This can be useful in situations where you want to continue processing with a default value in case of an error, without having to manually handle the error in a catch block.

### Difference between `doOnErrorResume` and `doOnErrorReturn`
The `doOnErrorResume` and `doOnErrorReturn` operators are both used to handle errors in a reactive stream. However, there's a difference in how they handle errors:

* `doOnErrorResume`: This operator takes a `Function` as an argument that maps the error to a new `Publisher` or `Mono` that will be used as a replacement for the original source. The new source will continue the emission of the reactive stream. In other words, `doOnErrorResume` resumes the stream processing with a new source in case of an error.

* `doOnErrorReturn`: This operator takes a fallback value as an argument that will be returned in case of an error. The reactive stream will emit the fallback value and terminate. In other words, `doOnErrorReturn` returns a fallback value in case of an error and terminates the stream.

So, the main difference between `doOnErrorResume` and `doOnErrorReturn` is that `doOnErrorResume` resumes the stream processing with a new source, while `doOnErrorReturn` returns a fallback value and terminates the stream. Choose between the two based on whether you want to continue processing the stream or not in case of an error.

### The `first`, `last`, and `take` operators

The first, last, and take operators are operators in the Reactor library for processing reactive streams in Spring.

* `first`: The `first` operator returns the first element in a reactive stream, or an empty Mono if the stream is empty.

* `last`: The `last` operator returns the last element in a reactive stream, or an empty Mono if the stream is empty.

* `take`: The `take` operator returns the first n elements in a reactive stream. If the stream contains fewer than n elements, all elements in the stream will be returned.

These operators are used to limit the number of elements that are processed in a reactive stream, and to retrieve specific elements from a reactive stream.

Here's an example of using the `first`, `last`, and `take` operators in a Spring Boot application:
```java
@RestController
public class ExampleController {

  private final ReactiveMongoTemplate template;

  public ExampleController(ReactiveMongoTemplate template) {
    this.template = template;
  }

  @GetMapping("/data/first")
  public Mono<Data> getFirstData() {
    return template.find(Query.empty(), Data.class)
      .first();
  }

  @GetMapping("/data/last")
  public Mono<Data> getLastData() {
    return template.find(Query.empty(), Data.class)
      .last();
  }

  @GetMapping("/data/take/{n}")
  public Flux<Data> getTakeData(@PathVariable int n) {
    return template.find(Query.empty(), Data.class)
      .take(n);
  }
}
```

### .retry() 
`.retry` is a method in the Reactor library that can be used to automatically retry a failed `Mono` or `Flux` sequence. It can be used to handle temporary errors or timeouts by retrying the sequence a specified number of times before giving up and completing the sequence with an error.

Here's an example of how to use the `.retry` method:
```java
Flux.just(1, 2, 3)
    .map(i -> {
        if (i == 2) {
            throw new RuntimeException("error");
        }
        return i;
    })
    .retry(1)
    .subscribe(System.out::println, System.err::println);
```
In this example, the `Flux` is generating numbers from 1 to 3. If the number is 2, it throws a `RuntimeException` with the message `"error"`. The `.retry` method is then used to retry the sequence once in case of an error. So, when the number 2 is encountered and an error is thrown, the sequence is retried and this time it will produce the number 3 and complete successfully. The result will be the numbers 1 and 3 printed to the console.





















