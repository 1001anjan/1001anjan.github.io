---
layout: default
title: Getting Started Spring Reactor
parent: Spring Reactor
grand_parent: Spring Boot
nav_order: 1
---
# Getting Started Spring Reactor

### Mono 
Mono in Spring Reactor is a reactive programming type representing a stream of zero or one element. It is part of the Reactive Streams specification and is used in Spring Reactor to handle non-blocking and asynchronous processing of data. It can be used to return a single value, error or completion signal to the subscriber. With Mono, you can create, compose, and manipulate reactive streams of data in a non-blocking manner, making it a great fit for modern, asynchronous systems.

### Here's a simple example of how to use Mono in Spring Boot:
```java
@RestController
public class ExampleController {

    @GetMapping("/example")
    public Mono<String> exampleEndpoint() {
        return Mono.just("Hello from Spring Boot!");
    }
}
```
In this example, the `exampleEndpoint` method returns a `Mono` object containing a single string value "Hello from Spring Boot!". When this endpoint is called, the returned Mono will emit the string to the subscriber, which in this case will be sent as the response to the HTTP request.

You can also use `Mono` to handle more complex scenarios, such as making `asynchronous` API calls, processing and transforming data, and handling errors.

### Mono.just
`Mono.just` is a factory method used to create a `Mono` that emits a single item. It is a convenient way to wrap a single value into a reactive stream that can be processed asynchronously.

For example, you can use `Mono.just` to return a single string, number, or object as the response to an HTTP request:
```java
@GetMapping("/example")
public Mono<String> exampleEndpoint() {
    return Mono.just("Hello from Spring Boot!");
}
```
In this example, the `Mono.just` method is used to create a `Mono` containing the string "Hello from Spring Boot!". When this endpoint is called, the Mono will emit the string to the subscriber, which in this case will be sent as the response to the HTTP request.

You can also use `Mono.just` to create a Mono that emits a custom object, like this:
```java
@GetMapping("/user")
public Mono<User> getUser() {
        User user = new User("John Doe", "john.doe@example.com");
        return Mono.just(user);
        }
```
In this example, a User object is created and wrapped in a Mono using `Mono.just`. When this endpoint is called, the `Mono` will emit the User object to the subscriber, which in this case will be sent as the response to the HTTP request.

### Flux
To send a list of objects as the response to an HTTP request in Spring Boot, you can use the `Flux` type. `Flux` is a reactive type that represents a stream of zero or more elements. It is also part of the Reactive Streams specification and is used in Spring Reactor to handle `non-blocking` and `asynchronous` processing of data.

Here's an example of how to send a list of User objects as the response to an HTTP request:

```java
@GetMapping("/users")
public Flux<User> getUsers() {
    List<User> users = Arrays.asList(
        new User("John Doe", "john.doe@example.com"),
        new User("Jane Doe", "jane.doe@example.com"),
        new User("Jim Smith", "jim.smith@example.com")
    );
    return Flux.fromIterable(users);
}
```
In this example, a list of `User` objects is created and wrapped in a `Flux` using the `Flux.fromIterable` method. When this endpoint is called, the `Flux` will emit each User object to the subscriber, one by one, as a stream of data. The subscriber will receive the list of User objects as the response to the HTTP request.

###  Flux.fromIterable
`Flux.fromIterable` is a factory method used to create a `Flux` from an `Iterable` object, such as a List. It allows you to wrap an `Iterable` object into a reactive stream that can be processed asynchronously.

For example, if you have a list of `User` objects and you want to send this list as the response to an HTTP request, you can use `Flux.fromIterable` to wrap the list in a `Flux`, like this:

```java
@GetMapping("/users")
public Flux<User> getUsers() {
    List<User> users = Arrays.asList(
        new User("John Doe", "john.doe@example.com"),
        new User("Jane Doe", "jane.doe@example.com"),
        new User("Jim Smith", "jim.smith@example.com")
    );
    return Flux.fromIterable(users);
}
```
In this example, the `Flux.fromIterable` method is used to create a `Flux` containing the list of `User` objects. When this endpoint is called, the `Flux` will emit each User object to the subscriber, one by one, as a stream of data. The subscriber will receive the list of User objects as the response to the HTTP request.

`Flux.fromIterable` is a convenient way to wrap an `Iterable` object into a reactive stream, allowing you to process its elements `asynchronously` and `non-blockingly`.

### Note:
In Spring Boot, the service layer is typically responsible for implementing the business logic of your application. Here's an example of a simple service layer implementation:

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public Flux<User> getAllUsers() {
        return userRepository.findAll();
    }

    public Mono<User> getUserById(String id) {
        return userRepository.findById(id);
    }

    public Mono<User> createUser(User user) {
        return userRepository.save(user);
    }

    public Mono<Void> deleteUser(String id) {
        return userRepository.deleteById(id);
    }
}
```
In this example, the `UserService` class is annotated with `@Service`, which is a stereotype annotation indicating that this class is a service layer component. The service layer component is responsible for implementing the business logic of the application.

The `UserService` class has a constructor that takes a `UserRepository` as an argument. The `UserRepository` is an interface that extends `ReactiveCrudRepository`, which provides basic CRUD operations for reactive data access.

The `UserService` class provides several methods that implement the business logic of the application, such as `getAllUsers`, which returns a list of all users, `getUserById`, which returns a single user by its ID, `createUser`, which creates a new user, and `deleteUser`, which deletes a user by its ID.

In this example, the methods return reactive types, such as `Flux` or `Mono`, to represent `asynchronous` and `non-blocking` data processing. The reactive types are returned by the methods of the `UserRepository` interface, which is used by the service layer to access the data stored in the database.

### Note 2:
Here's an example of a service layer method that makes multiple HTTP requests and combines the results into a custom object:

```java
@Service
public class UserService {

    private final WebClient webClient;

    public UserService(WebClient webClient) {
        this.webClient = webClient;
    }

    public Mono<UserProfile> getUserProfile(String userId) {
        return Mono.zip(
            webClient.get().uri("/user/{userId}", userId).retrieve().bodyToMono(User.class),
            webClient.get().uri("/user/{userId}/posts", userId).retrieve().bodyToFlux(Post.class),
            webClient.get().uri("/user/{userId}/comments", userId).retrieve().bodyToFlux(Comment.class),
            (user, posts, comments) -> {
                UserProfile userProfile = new UserProfile(user, posts, comments);
                return userProfile;
            }
        );
    }
}
```
In this example, the `UserService` class has a constructor that takes a `WebClient` as an argument. The `WebClient` is a reactive HTTP client provided by Spring `Webflux` that allows you to make `non-blocking` HTTP requests.

The `getUserProfile` method makes three HTTP requests to different endpoints using the `WebClient`. The first request is to retrieve the user information, the second request is to retrieve the posts made by the user, and the third request is to retrieve the comments made by the user.

The `Mono.zip` method is used to combine the results of the three HTTP requests into a custom `UserProfile` object. The `zip` method takes three `Monos` as arguments and returns a single `Mono` that contains the result of combining the three Monos. In this case, the result of the `zip` method is a `Mono` that contains a `UserProfile` object, which is created by the lambda expression passed as the fourth argument to the `zip` method.

When the `getUserProfile` method is called, it makes three `asynchronous` HTTP requests, combines the results of the requests into a `UserProfile` object, and returns the `UserProfile` as a `Mono`. This allows the service layer to make multiple HTTP requests and combine the results into a custom object in a `non-blocking` and `asynchronous` manner.

### Note 3:
Here's an example of a service layer method that calls one HTTP request, then based on the result, calls another HTTP request, and finally returns the result:
```java
@Service
public class UserService {

    private final WebClient webClient;
    private final AnotherService anotherService;

    public UserService(WebClient webClient, AnotherService anotherService) {
        this.webClient = webClient;
        this.anotherService = anotherService;
    }

    public Mono<Result> getResult(String userId) {
        return webClient.get().uri("/user/{userId}", userId).retrieve().bodyToMono(User.class)
            .flatMap(user -> 
                anotherService.getData(user.getData())
                    .flatMap(data -> 
                        webClient.get().uri("/user/{userId}/data", user.getData()).retrieve().bodyToMono(Data.class)
                            .map(data -> {
                                Result result = new Result(user, data);
                                return result;
                            })
                    )
            );
    }
}
```
In this example, the `UserService` class has a constructor that takes a `WebClient` and another `AnotherService` as arguments. The `WebClient` is a reactive HTTP client provided by Spring Webflux that allows you to make `non-blocking` HTTP requests. The `AnotherService` is another service that provides some business logic.

The `getResult` method makes one HTTP request to retrieve the user information using the `WebClient`. The result of the first HTTP request is a Mono containing the user information. The `flatMap` operator is used to chain the second HTTP request and the call to the `AnotherService`.

The second HTTP request is made using the `flatMap` operator and the `user.getData()` method, which retrieves the data from the first HTTP request. The result of the second HTTP request is a Mono containing the data.

The `AnotherService.getData` method is called using the `flatMap` operator, and the result is a `Mono` containing the data processed by the `AnotherService`.

The third HTTP request is made using the `flatMap` operator and the `user.getData()` method, which retrieves the data from the first HTTP request. The result of the third HTTP request is a `Mono` containing the data.

The `map` operator is used to combine the results of the three steps into a single Result object

