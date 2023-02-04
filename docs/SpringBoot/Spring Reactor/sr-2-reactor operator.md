---
layout: default
title: Reactor Operator
parent: Spring Reactor
grand_parent: Spring Boot
nav_order: 2
---
# Reactor Operator
Here is a list of some of the most commonly used reactive operators in Spring Reactor:

1. `map` - transforms the elements emitted by a reactive type into another type.
2. `flatMap` - transforms a `Mono` into another `Mono` by applying a function to each element in the source `Mono`.
3. `flatMapMany` - transforms a `Mono` into a `Flux` by applying a function to each element in the source `Mono` and concatenating the resulting `Flux` with the `Flux` emitted by other elements.
4. `filter` - filters elements emitted by a reactive type based on a given predicate.
5. `zipWith` - combines elements emitted by two reactive types into a single stream by applying a function to each pair of elements.
6. `reduce` - reduces a `Flux` into a single value by applying a binary operator to each element.
7. `take` - limits the number of elements emitted by a reactive type.
8. `first` - returns the first element emitted by a reactive type.
9. `last` - returns the last element emitted by a reactive type.
10. `doOnNext` - performs an action for each element emitted by a reactive type.
11. `doOnError` - performs an action when an error occurs in a reactive type.
12. `onErrorResume` - returns a fallback reactive type if an error occurs in the source reactive type.
13. `onErrorReturn` - returns a default value if an error occurs in a reactive type.
14. `retry` - retries a reactive type if an error occurs.

This is not an exhaustive list and there are many more operators available in Spring Reactor. These operators can be combined in various ways to build complex reactive processing pipelines.

### flatMap
`flatMap` is a reactive stream operator in Spring Reactor that transforms the elements emitted by a source Publisher into multiple Publishers and then flattens the elements from those into a single stream of values.

You can use `flatMap` when you have a reactive stream and you need to perform an operation on each element that results in a stream of values, and then you want to flatten the results of those streams into a single stream of values.

For example, you can use `flatMap` to perform multiple database queries for each item in a stream and then combine the results into a single stream of values.

### Here is a simple example that demonstrates how to use flatMap in Spring Reactor:
```java
import reactor.core.publisher.Flux;

public class FlatMapExample {
    public static void main(String[] args) {
        Flux<String> source = Flux.just("A", "B", "C", "D", "E");

        source.flatMap(s -> Flux.fromArray(s.split("")))
                .subscribe(System.out::println);
    }
}
```
In this example, the `flatMap` operator transforms the source `Flux`, which emits 5 strings, into multiple `Flux` instances that emit individual characters from each string. The resulting `Flux` is then flattened into a single stream of characters, which are printed to the console.

The output of this program would be:
```css
A
B
C
D
E
```

### Here's an example of using flatMap in a Spring Boot application:
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Flux;

@RestController
public class FlatMapExampleController {

    @GetMapping("/words")
    public Flux<String> getWords() {
        return Flux.just("Hello", "World")
                .flatMap(word -> Flux.fromArray(word.split("")));
    }
}
```
n this example, the `getWords` method returns a `Flux` of strings representing the characters in the words "Hello" and "World". The `flatMap` operator is used to split each word into its individual characters and return a Flux of those characters.

When you access the endpoint `/words`, you will receive a stream of characters representing the two words. For example:

```yaml
H
e
l
l
o
W
o
r
l
d
```
`flatMap` is used to transform a reactive stream into another stream that contains the values of the inner streams created by the `flatMap` operation. It allows you to perform an operation on each item in a reactive stream that results in another stream, and then combines all of the inner streams into a single stream of values.

Here are some common use cases for `flatMap`:

1. Asynchronous operations: When you need to perform an asynchronous operation on each item in a reactive stream, you can use flatMap to turn the results of that operation into another stream and then flatten the results.

2. Transformation of data: If you have a reactive stream of data and you need to perform some operation on each item that results in a new set of data, you can use flatMap to transform the data and create a new stream of values.

3. Parallel processing: If you have a reactive stream and you need to perform an operation on each item in parallel, you can use `flatMap` to split the stream into multiple streams and then combine the results.

4. Event-driven processing: If you have a reactive stream of events and you need to perform an operation on each event that results in another stream of events, you can use `flatMap` to flatten the results into a single stream of events.

In summary, `flatMap` is a powerful operator that enables you to perform operations on reactive streams, create new streams, and flatten the results into a single stream of values.

### The map operator
The `map` operator is a reactive stream operator in Reactive Programming that is used to transform the elements of a reactive stream into new elements. The map operator applies a function to each element in a reactive stream and returns a new reactive stream that contains the results of the function applied to each element.

Here is a simple example that demonstrates how to use the `map` operator:

```java
import reactor.core.publisher.Flux;

public class MapExample {
    public static void main(String[] args) {
        Flux<Integer> source = Flux.just(1, 2, 3, 4, 5);

        source.map(i -> i * 2)
                .subscribe(System.out::println);
    }
}
```
In this example, the `map` operator takes a `Flux` of integers and applies a function that multiplies each integer by 2. The resulting Flux is then subscribed to and the results are printed to the console.

The output of this program would be:
```yaml
2
4
6
8
10
```
So, the `map` operator is used to transform the elements of a reactive stream into new elements using a function. The function is applied to each element in the stream and the results are returned in a new reactive stream.

### The main difference between flatMap and map
The main difference between `flatMap` and `map` is the structure of the resulting reactive stream.

The `map` operator transforms the elements of a reactive stream into new elements using a function. The function is applied to each element in the stream and the results are returned in a new reactive stream. The resulting reactive stream has the same number of elements as the original stream.

The `flatMap` operator, on the other hand, transforms each element of a reactive stream into a new reactive stream using a function, and then combines all the inner streams into a single reactive stream of values. The resulting reactive stream can have a different number of elements than the original stream.

Here is an example that demonstrates the difference between `flatMap` and `map`:
```java
import reactor.core.publisher.Flux;

public class MapAndFlatMapExample {
    public static void main(String[] args) {
        Flux<String> source = Flux.just("A", "B", "C", "D", "E");

        source.map(s -> s.split(""))
                .subscribe(System.out::println);

        source.flatMap(s -> Flux.fromArray(s.split("")))
                .subscribe(System.out::println);
    }
}
```
In this example, the first subscribe call uses the `map` operator to split each string in the source `Flux` into an array of characters. The resulting `Flux` is a stream of arrays of characters.

The second subscribe call uses the `flatMap` operator to split each string in the source `Flux` into an array of characters and then flatten the resulting streams into a single stream of characters.

The output of this program would be:

```yaml
[A]
[B]
[C]
[D]
[E]
A
B
C
D
E
```
### Here is an example of using flatMap in a Spring Boot application:
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Flux;

@RestController
public class FlatMapExampleController {
    @GetMapping("/flatmap")
    public Flux<String> getFlattenedStrings() {
        Flux<String> source = Flux.just("A", "B", "C", "D", "E");

        return source.flatMap(s -> Flux.fromArray(s.split("")));
    }
}
```
In this example, a REST endpoint is defined using the `@RestController` annotation. The `getFlattenedStrings` method returns a `Flux` of strings that have been transformed using the `flatMap` operator. The `flatMap` operator splits each string in the source `Flux` into an array of characters and then flattens the resulting streams into a single stream of characters.

The endpoint can be accessed using a web client such as curl or a browser, and the result will be a stream of flattened characters.

### Here is an example of a method that returns a Mono<Void> in Spring Boot:
```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class VoidExampleController {
    @PostMapping("/void")
    public Mono<Void> doSomething() {
        // Perform some action here

        return Mono.empty();
    }
}
```
In this example, a REST endpoint is defined using the `@RestController` annotation. The `doSomething` method returns a `Mono<Void>`, indicating that the endpoint does not return any data. The `Mono.empty()` method is used to create an empty `Mono` that represents a `Void` type.

The `@PostMapping` annotation is used to specify that this endpoint should be accessed using an HTTP POST request. When this endpoint is accessed, it will perform some action and return a `Void` type, indicating that no data is returned.

### The .when and .then methods 
The `.when` and `.then` methods in Spring Reactor are used to perform operations based on the results of a reactive stream.

The `.when` method is used to conditionally perform an operation based on the value of a reactive stream. For example, you can use the `.when` method to perform an operation only when a certain condition is met.

The `.then` method is used to perform an operation after a reactive stream has completed. For example, you can use the `.then` method to perform an action after a stream of data has been processed.

Here is an example of using the `.when` and `.then` methods in Spring Reactor:
```java
import reactor.core.publisher.Mono;

Mono<Integer> source = Mono.just(10);

source.when(s -> s > 5)
      .then(s -> System.out.println("Value is greater than 5"))
      .thenEmpty(Mono.empty());
```
In this example, the source `Mono` contains a single value of 10. The .when method is used to perform a conditional operation based on the value of the source stream. In this case, the condition is that the value should be greater than 5. If the condition is met, the `.then` method is used to print a message to the console. The `.thenEmpty` method is used to complete the reactive stream and return an empty `Mono`.

### Here is an example of using the .when and .then methods in a Spring Boot application:
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class WhenThenExampleController {
    @GetMapping("/when-then")
    public Mono<Void> doSomething() {
        Mono<Integer> source = Mono.just(10);

        return source.when(s -> s > 5)
                    .then(s -> System.out.println("Value is greater than 5"))
                    .thenEmpty(Mono.empty());
    }
}
```
In this example, a REST endpoint is defined using the `@RestController` annotation. The `doSomething` method returns a `Mono<Void>`, indicating that the endpoint does not return any data.

The source `Mono` contains a single value of 10. The `.when` method is used to perform a conditional operation based on the value of the source stream. In this case, the condition is that the value should be greater than 5. If the condition is met, the `.then` method is used to print a message to the console. The `.thenEmpty` method is used to complete the reactive stream and return an empty `Mono`.

The endpoint can be accessed using an HTTP GET request to `/when-then`. When the endpoint is accessed, the doSomething method will be executed and the reactive stream will be processed, printing a message to the console if the value is greater than 5.

### A functional interface is an interface in Java
A functional interface is an interface in Java that has exactly one abstract method. Functional interfaces are used in Java 8 and later to create functional programming constructs, such as lambda expressions and method references.

Here's an example of how to use a functional interface in Java:

```java
import java.util.function.Consumer;

public class Example {
    public static void main(String[] args) {
        Consumer<String> printString = s -> System.out.println(s);
        printString.accept("Hello World");
    }
}
```
In this example, the `Consumer` interface is a functional interface defined in the `java.util.function` package. It has a single abstract method void `accept(T t)`.

A lambda expression is used to create an instance of the `Consumer` interface, which is then assigned to the variable `printString`. The accept method of the `Consumer` interface is then used to print the string "Hello World" to the console.

You can use functional interfaces in conjunction with lambda expressions and method references to create concise and readable code, especially when working with streams and reactive programming constructs in Java.

### Here's an example of how to use functional interfaces in a Spring Boot application:
```java
import java.util.function.Function;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class FunctionExampleController {
    @GetMapping("/square/{number}")
    public Mono<Integer> squareNumber(@PathVariable int number) {
        Function<Integer, Integer> square = x -> x * x;
        return Mono.just(square.apply(number));
    }
}
```
In this example, a REST endpoint is defined using the `@RestController` annotation. The `squareNumber` method takes a number as a path variable, squares it using a `Function` and returns the result as a `Mono`.

The `Function` interface is a functional interface defined in the `java.util.function` package. It has a single abstract method `R apply(T t)`, where `R` is the return type and `T` is the input type.

In the example, a lambda expression is used to create an instance of the `Function` interface, which is then assigned to the variable `square`. The `apply` method of the `Function` interface is then used to square the number passed as an argument to the endpoint.

### There are several advantages of using functional interfaces in Java:
1. Increased readability: Functional interfaces and lambda expressions can make your code more concise and readable, especially when working with streams and reactive programming constructs.

2. Improved performance: Using functional interfaces and lambda expressions can improve the performance of your code, especially when working with parallel streams or reactive programming.

3. Simplified code: Functional interfaces allow you to define functionality as a single abstract method, which can simplify your code and make it easier to understand.

4. Improved flexibility: By using functional interfaces, you can create a more flexible codebase that is easier to maintain and extend. For example, you can define an interface with a single abstract method, and then provide different implementations of that method for different use cases.

5. Better type inference: Java 8 and later versions support improved type inference, which allows the compiler to automatically determine the types of arguments and return values when working with functional interfaces and lambda expressions.

Overall, functional interfaces and lambda expressions are a powerful tool for creating concise and readable code in Java, and can help you write better and more performant code, especially when working with streams and reactive programming constructs.

```java
import java.util.function.Function;
import java.util.function.Supplier;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

@RestController
public class ComplexExampleController {
    @GetMapping("/employee/{id}")
    public Mono<Employee> getEmployee(@PathVariable String id) {
        // First, we retrieve the employee data
        Mono<EmployeeData> employeeData = retrieveEmployeeData(id);

        // Then, we use flatMap to retrieve the employee's department
        Mono<Department> department = employeeData.flatMap(data -> retrieveDepartment(data.getDepartmentId()));

        // Finally, we use map to create the final Employee object
        return Mono.zip(employeeData, department, this::createEmployee);
    }

    private Mono<EmployeeData> retrieveEmployeeData(String id) {
        return Mono.just(new EmployeeData(id, "John Doe", "123456"));
    }

    private Mono<Department> retrieveDepartment(String departmentId) {
        return Mono.just(new Department(departmentId, "IT"));
    }

    private Employee createEmployee(EmployeeData employeeData, Department department) {
        return new Employee(employeeData.getId(), employeeData.getName(), department.getName());
    }

    @GetMapping("/employees")
    public Flux<Employee> getAllEmployees() {
        // First, we retrieve a list of employee IDs
        Flux<String> employeeIds = retrieveEmployeeIds();

        // Then, we use flatMap to retrieve the data for each employee
        Flux<EmployeeData> employeeData = employeeIds.flatMap(this::retrieveEmployeeData);

        // Next, we use map to retrieve the departments for each employee
        Flux<Department> departments = employeeData.flatMap(data -> retrieveDepartment(data.getDepartmentId()));

        // Finally, we use map to create the final Employee objects
        return Flux.zip(employeeData, departments, this::createEmployee);
    }

    private Flux<String> retrieveEmployeeIds() {
        return Flux.just("1", "2", "3", "4");
    }

    private static class EmployeeData {
        private String id;
        private String name;
        private String departmentId;

        public EmployeeData(String id, String name, String departmentId) {
            this.id = id;
            this.name = name;
            this.departmentId = departmentId;
        }

        public String getId() {
            return id;
        }

        public String getName() {
            return name;
        }

        public String getDepartmentId() {
            return departmentId;
        }
    }

    private static class Department {
        private String id;
        private String name;

    }
}
```
### Mono.supplier
`Mono.supplier` is a static method in the Reactor library that creates a new Mono from a `Supplier` instance.

A `Supplier` is a functional interface defined in the Java standard library that represents a supplier of results. It has a single abstract method, `get`, that returns a result of a specified type.

When using `Mono.supplier`, the `Supplier` instance is used to generate the data that will be emitted by the Mono. The get method of the `Supplier` is called when the `Mono` is subscribed to, and the result is emitted as a single item.

Here's an example of using `Mono.supplier` to create a `Mono` that emits the result of a `Supplier`:

```java
Supplier<String> stringSupplier = () -> "Hello, World!";
        Mono<String> helloWorld = Mono.fromSupplier(stringSupplier);
```

In this example, the `stringSupplier` instance is a `Supplier` that returns the string `"Hello, World!"`. The `Mono.fromSupplier` method is used to create a `Mono` that emits the result of the `stringSupplier` when subscribed to.

```java
@RestController
public class UserController {
  
  private final UserService userService;
  
  public UserController(UserService userService) {
    this.userService = userService;
  }
  
  @GetMapping("/users/{id}")
  public Mono<ResponseEntity<User>> getUserById(@PathVariable Long id) {
    return Mono.fromSupplier(() -> userService.findById(id))
        .map(user -> ResponseEntity.ok(user))
        .defaultIfEmpty(ResponseEntity.notFound().build());
  }
}
```
In this example, the `UserController` class is a REST controller that retrieves a user by ID and returns the result as a `Mono` of `ResponseEntity<User>`. The `userService.findById` method is used to retrieve the user from a database, and it returns the result as an optional.

The `Mono.fromSupplier` method is used to create a `Mono` from a `Supplier` that retrieves the user from the database. The `map` operator is used to map the optional to a `ResponseEntity` with a 200 status code if the user is found, or a 404 status code if the user is not found. The `defaultIfEmpty` operator is used to provide the default value of `ResponseEntity.notFound().build()` if the optional is empty.

### Note 1:
If you don't use `Mono.supplier`, you would need to use a different method to create a `Mono` that emits the result of a method or operation that returns a value.

For example, if you have a method that returns a `User` object, you could create a `Mono` from the result of that method using the `Mono.just` method:

```java
@RestController
public class UserController {
  
  private final UserService userService;
  
  public UserController(UserService userService) {
    this.userService = userService;
  }
  
  @GetMapping("/users/{id}")
  public Mono<ResponseEntity<User>> getUserById(@PathVariable Long id) {
    User user = userService.findById(id);
    return Mono.just(ResponseEntity.ok(user));
  }
}
```
In this example, the `userService.findById` method is used to retrieve the user from the database, and the `Mono.just` method is used to create a `Mono` that emits the result as a single item. Note that this approach assumes that the user is always present and doesn't handle the case where the user is not found.

Another option is to use the `Mono.defer` method, which creates a `Mono` that evaluates the provided `Mono` supplier only when the Mono is subscribed to:
```java
@RestController
public class UserController {
  
  private final UserService userService;
  
  public UserController(UserService userService) {
    this.userService = userService;
  }
  
  @GetMapping("/users/{id}")
  public Mono<ResponseEntity<User>> getUserById(@PathVariable Long id) {
    return Mono.defer(() -> {
      User user = userService.findById(id);
      return Mono.just(ResponseEntity.ok(user));
    });
  }
}
```
In this example, the `Mono.defer` method is used to create a `Mono` that evaluates the `Mono.just` method only when the `Mono` is subscribed to. This approach allows you to defer the evaluation of the method that retrieves the user until the `Mono` is subscribed to, which can be useful in certain scenarios.

`Mono.just` and `Mono.supplier` are two methods used to create a `Mono` in Spring Reactor.

`Mono.just` is used to create a `Mono` that emits a single item. The item is specified as an argument when calling the `Mono.just` method:

```java
Mono<String> mono = Mono.just("Hello");
```
`Mono.supplier` is used to create a `Mono` that emits the result of a method or operation that returns a value. The method or operation is specified as a `Supplier` when calling the `Mono.supplier` method:

```java
Mono<String> mono = Mono.fromSupplier(() -> "Hello");
```
In general, `Mono.just` is used when you have a value that is known at the time of creation and `Mono.supplier` is used when the value is not known until the `Mono` is subscribed to. This can be useful in scenarios where you want to defer the evaluation of a method or operation until the `Mono` is subscribed to, for example, when making a network request.

There is a similar method in `Flux` as `Mono.supplier`, it's called `Flux.from`. `Flux.from` is used to create a `Flux` that emits the elements of an `Iterable`, `Array`, or `Publisher`. It can be used as a way to create a `Flux` that emits the results of a method or operation that returns multiple values:

```java
Flux<String> flux = Flux.fromIterable(Arrays.asList("Hello", "world"));
```
```java
Flux<Integer> flux = Flux.fromArray(new Integer[] {1, 2, 3});
```
In general, `Flux.from` is used when you have a collection of values that is known at the time of creation. Like `Mono.supplier`, it is also useful in scenarios where you want to defer the evaluation of a method or operation until the `Flux` is subscribed to, for example, when making a network request that returns multiple values.

### Here's an example of how you can call a method that returns a `List` of objects using `Flux` in Spring Reactor:

```java
public List<Object> getObjectList() {
    return Arrays.asList(new Object(), new Object(), new Object());
}

...

Flux<Object> objectFlux = Flux.fromIterable(getObjectList());

```
In this example, the `getObjectList` method returns a `List` of `Object` instances. To use this method with `Flux`, you can call `Flux.fromIterable` and pass in the result of `getObjectList` as the argument. This creates a `Flux` that emits each of the objects in the List.

### Here's an example of how you can use `Flux` in a Spring Boot application:
```java
@RestController
public class MyController {

    @GetMapping("/objects")
    public Flux<Object> getObjects() {
        return Flux.fromIterable(getObjectList());
    }

    private List<Object> getObjectList() {
        return Arrays.asList(new Object(), new Object(), new Object());
    }
}
```

### Here's an example of how you can use `Mono` and `Flux` to make multiple database calls in a Spring Boot application:

```java
@RestController
public class MyController {

    private final UserRepository userRepository;
    private final OrderRepository orderRepository;

    public MyController(UserRepository userRepository, OrderRepository orderRepository) {
        this.userRepository = userRepository;
        this.orderRepository = orderRepository;
    }

    @GetMapping("/user/{id}")
    public Mono<User> getUser(@PathVariable String id) {
        return userRepository.findById(id);
    }

    @GetMapping("/user/{id}/orders")
    public Flux<Order> getUserOrders(@PathVariable String id) {
        return userRepository.findById(id)
                .flatMapMany(user -> orderRepository.findByUserId(user.getId()));
    }
}
```
In this example, we have a `RestController` with two endpoints. The `getUser` endpoint takes an id parameter and returns a single `User` instance from the database using the `UserRepository`. The `getUserOrders` endpoint takes an id parameter and returns a stream of `Order` instances from the database using the `OrderRepository`.

The `getUserOrders` endpoint makes two database calls: first, it retrieves a single `User` instance using `UserRepository.findById`, and then it retrieves a stream of `Order` instances using `OrderRepository.findByUserId`, passing in the id of the `User` instance. The `flatMapMany` operator is used to flatten the `Mono<User>` returned by `UserRepository.findById` into a `Flux<Order>`. This allows us to make two database calls and return the results as a single stream.

### `flatMapMany `
`flatMapMany` is a reactive operator that is used in Spring Reactor to convert a reactive type into another reactive type. It is used in combination with `Mono` to convert a `Mono<T>` into a `Flux<R>` by applying a function to each element emitted by the source `Mono`, and returning the elements as a `Flux`.

The function passed to `flatMapMany` takes the single `T` emitted by the source `Mono` and returns a `Flux<R>` which represents a stream of values of type `R`. The resulting `Flux<R>` is then concatenated with the `Flux` emitted by other elements.

The `flatMapMany` operator is useful when you want to perform an operation on each element of a reactive type, and return the results as a different reactive type. This can be useful when you want to make multiple database calls or perform other types of operations that return a stream of values. By using `flatMapMany`, you can chain these operations together and return a single stream of values to the client.

### The difference between `flatMap` and `flatMapMany`

The main difference between `flatMap` and `flatMapMany` in Spring Reactor is that `flatMap` is used to transform a `Mono` into another `Mono`, while `flatMapMany` is used to transform a `Mono` into a `Flux`.

`flatMap` takes a function that maps a single value emitted by the source `Mono` into another `Mono`. The resulting `Mono` is then merged into the original `Mono` stream, so that the elements of the two `Mono` streams are interleaved in the resulting stream.

`flatMapMany` takes a function that maps a single value emitted by the source `Mono` into a `Flux`. The resulting `Flux` is then concatenated with the `Flux` emitted by other elements in the source `Mono`.

In summary, `flatMap` is used when you want to perform a single operation on each element of a reactive type and return the result as a different reactive type, while `flatMapMany` is used when you want to perform multiple operations on each element of a reactive type and return the results as a stream of values.

#### Here is an example of using the `filter` operator in Spring Boot:
```java
@Service
public class UserService {

    public Flux<User> getAllUsers() {
        return Flux.just(
                new User(1, "John Doe"),
                new User(2, "Jane Doe"),
                new User(3, "Jim Smith"),
                new User(4, "Sarah Johnson")
        );
    }
}

@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public Flux<User> getUsers() {
        return userService.getAllUsers()
                .filter(user -> user.getId() % 2 == 0)
                .map(user -> {
                    user.setName(user.getName().toUpperCase());
                    return user;
                });
    }
}
```
In this example, the `UserService` returns a `Flux` of User objects. The `UserController` then filters the users with an even id and maps the filtered users to return their names in uppercase. The filtered and transformed users are then returned as a `Flux`.

### Here is an example of using the `subscribe` method in Spring Boot:

```java
@Service
public class UserService {

    public Flux<User> getAllUsers() {
        return Flux.just(
                new User(1, "John Doe"),
                new User(2, "Jane Doe"),
                new User(3, "Jim Smith"),
                new User(4, "Sarah Johnson")
        );
    }
}

@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public void getUsers() {
        userService.getAllUsers()
                .filter(user -> user.getId() % 2 == 0)
                .map(user -> {
                    user.setName(user.getName().toUpperCase());
                    return user;
                })
                .subscribe(user -> {
                    System.out.println("Received user: " + user);
                }, error -> {
                    System.err.println("Error occured: " + error);
                }, () -> {
                    System.out.println("All users received");
                });
    }
}
```
In this example, the `UserService` returns a `Flux` of `User` objects. The `UserController` then filters the users with an even id, maps the filtered users to return their names in uppercase, and subscribes to the `Flux`. When each user is received, it is printed to the console. In case of an error, the error is printed to the error console. Finally, when all users are received, a message is printed to the console indicating that all users have been received.

















