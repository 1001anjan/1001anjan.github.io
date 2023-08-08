---
layout: default
title: Java 8
parent: Quick Notes
grand_parent: Java
nav_order: 6
---
# Java 8 

Java 8, released in March 2014, introduced several significant features and enhancements to the Java programming language. Some of the main features of Java 8 include:

* Lambda Expressions: Lambda expressions allow you to write more concise and expressive code. They enable the functional programming style by treating functions as first-class citizens. With lambda expressions, you can pass behavior as arguments to methods or assign them to variables. They greatly simplify writing code using functional interfaces, such as `Predicate`, `Consumer`, and `Function`.

* Stream API: The Stream API provides a new abstraction for working with sequences of elements. Streams allow you to process collections of data in a functional and declarative manner. You can perform various operations, such as filtering, mapping, and reducing, on streams. Streams are designed to be efficient and can leverage parallel processing to take advantage of multiple cores.

* Default Methods: Default methods allow you to add new methods to existing interfaces without breaking the implementations of classes that implement those interfaces. This feature was introduced to support backward compatibility with existing code while allowing interfaces to evolve.

* Functional Interfaces: Java 8 introduced the @FunctionalInterface annotation, which indicates that an interface is intended to be used as a functional interface. A functional interface is an interface that has a single abstract method and can be used with lambda expressions. The java.util.function package provides a set of predefined functional interfaces, such as Predicate, Consumer, and Function.

* Method References: Method references allow you to refer to a method without executing it. They provide a shorthand syntax for lambda expressions and make the code more readable. Method references can be used when the lambda expression only calls an existing method, without any additional logic.

* Optional: The Optional class provides a container object that may or may not contain a non-null value. It encourages a more explicit and null-safe coding style by forcing developers to handle the possibility of null values explicitly. It helps avoid NullPointerExceptions and makes code more robust.

* Date/Time API: Java 8 introduced a new date and time API in the java.time package, which provides improved support for date and time manipulation. The new API is more intuitive, thread-safe, and offers better functionality for working with dates, times, intervals, and time zones.

These are some of the main features introduced in Java 8. They brought significant improvements to the language, making it more expressive, efficient, and flexible.

### Lambda Expression

A lambda expression in Java is a concise way to represent an anonymous function—a function that doesn't have a name and can be treated as a value. It allows you to pass behavior as an argument to methods or assign it to variables. Lambda expressions enable functional programming and can be used in various use cases where you need to work with functional interfaces.

Here's an example of a lambda expression:

```markdown
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// Using lambda expression to sort the names in ascending order
Collections.sort(names, (name1, name2) -> name1.compareTo(name2));

// Printing the sorted names
names.forEach(System.out::println);
```
Lambda expressions have several use cases:

* Functional Interfaces: Lambda expressions are commonly used with functional interfaces, which are interfaces that have a single abstract method. They allow you to pass behavior as an argument to methods that expect functional interfaces.

* Collection Processing: Lambda expressions work well with the Stream API introduced in Java 8. You can use lambda expressions to perform operations like filtering, mapping, and reducing on collections in a concise and declarative way.

* Event Handling: Lambda expressions can be used for event handling in graphical user interfaces (GUIs) or other event-driven applications. Instead of implementing a separate class for each event handler, you can use lambda expressions to define the behavior directly.

* Multithreading: Lambda expressions can be utilized to simplify multithreading code by expressing parallelizable tasks as functional interfaces.

Overall, lambda expressions provide a more expressive and concise way to write code, especially when working with functional interfaces and performing operations on collections or dealing with event-driven programming.


### Stream API

The Stream API in Java 8 provides a powerful set of functions for processing sequences of elements in a functional and declarative way. It offers several use cases and advantages, including:

* Collection Operations: The Stream API allows you to perform various operations on collections, such as filtering, mapping, sorting, and reducing. For example:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Example 1: Filtering even numbers
List<Integer> evenNumbers = numbers.stream()
                                   .filter(n -> n % 2 == 0)
                                   .collect(Collectors.toList());

// Example 2: Doubling the numbers
List<Integer> doubledNumbers = numbers.stream()
                                      .map(n -> n * 2)
                                      .collect(Collectors.toList());

// Example 3: Summing all numbers
int sum = numbers.stream()
                 .reduce(0, Integer::sum);
```

In these examples, the Stream API allows you to easily filter elements, transform them, and perform aggregations on the collection.

* Parallel Processing: The Stream API supports parallel processing, which means that operations can be executed concurrently on multiple threads. This can significantly improve performance when dealing with large datasets. You can use the `parallel()` method to convert a sequential stream to a parallel stream.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sum = numbers.parallelStream()
                 .reduce(0, Integer::sum);
```

In this example, the parallelStream() method is used to convert the stream to a parallel stream, and the reduction operation is performed concurrently.

* Lazy Evaluation: The Stream API uses lazy evaluation, which means that intermediate operations are only executed when required. This allows for efficient processing, especially when dealing with large datasets or infinite streams. Intermediate operations such as `filter()` and `map()` are not evaluated until a terminal operation, like `collect()` or `forEach()`, is called.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Example: Printing only the first three even numbers
numbers.stream()
       .filter(n -> n % 2 == 0)
       .limit(3)
       .forEach(System.out::println);
```
In this example, the filter() and limit() operations are only evaluated for the first three even numbers encountered.

* Code Readability and Conciseness: The Stream API provides a more expressive and concise way to write code for collection processing. It allows you to chain multiple operations together, making the code more readable and reducing the need for intermediate variables.
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// Example: Printing names in uppercase
names.stream()
     .map(String::toUpperCase)
     .forEach(System.out::println);
```
In this example, the `map()` operation is used to transform each name to uppercase before printing it.

The Stream API offers many more operations and functionalities, such as grouping, partitioning, flat-mapping, and more. It simplifies collection processing, promotes a functional programming style, and provides performance benefits through parallel processing and lazy evaluation.



# The Optional class
The `Optional` class in Java is part of the java.util package and was introduced in Java 8. It is used to represent an optional value, which can be either present or absent. The main purpose of Optional is to avoid `NullPointerException` by explicitly indicating the possibility of a value being absent.

Here's an example to illustrate the use of `Optional`:
```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        String name = "John Doe";
        Optional<String> optionalName = Optional.of(name);

        // Checking if the value is present
        if (optionalName.isPresent()) {
            System.out.println("Name is present: " + optionalName.get());
        } else {
            System.out.println("Name is absent");
        }

        // Performing an action if the value is present
        optionalName.ifPresent(n -> System.out.println("Hello, " + n));

        // Using a default value if the value is absent
        String defaultValue = "Guest";
        String result = optionalName.orElse(defaultValue);
        System.out.println("Result: " + result);

        // Transforming the value with a mapping function
        String transformed = optionalName.map(n -> "Mr. " + n).orElse(defaultValue);
        System.out.println("Transformed: " + transformed);

        // Using a supplier to provide a default value if the value is absent
        String supplied = optionalName.orElseGet(() -> "Unknown");
        System.out.println("Supplied: " + supplied);

        // Throwing an exception if the value is absent
        String value = optionalName.orElseThrow(() -> new IllegalArgumentException("Name is required"));
    }
}
```
In this example, an `Optional<String>` named optionalName is created with the value "John Doe" using `Optional.of(name)`.

* The `isPresent()` method is used to check if the value is present, and `get()` retrieves the value if it is present.

* The `ifPresent()` method allows performing an action if the value is present.

* The `orElse()` method returns a default value if the value is absent.

* The `map()` method transforms the value using a mapping function.

* The `orElseGet()` method provides a default value using a supplier if the value is absent.

* The `orElseThrow()` method throws an exception if the value is absent.

* By using `Optional`, you can handle cases where a value might be absent and design your code accordingly. It encourages explicit handling of nullable values and provides a more expressive and safer way to work with potentially absent values, reducing the chances of `NullPointerExceptions`.

