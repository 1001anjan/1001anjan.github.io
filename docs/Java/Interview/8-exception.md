---
layout: default
title: Exception
parent: Interview Preparation
grand_parent: Java
nav_order: 8
---
### What is the difference between checked and unchecked exceptions in Java? Provide examples of each.
In Java, exceptions are categorized into two types: checked exceptions and unchecked exceptions.

### Checked Exceptions:
Checked exceptions are the exceptions that must be declared in the method signature using the `throws` keyword or handled using a try-catch block. The compiler enforces the handling or declaring of checked exceptions at compile-time. Examples of checked exceptions include `IOException`, `SQLException`, and `ClassNotFoundException`.

Example:
```java
import java.io.FileReader;
import java.io.IOException;

public class FileHandler {
    public void readFile(String fileName) throws IOException {
        FileReader fileReader = new FileReader(fileName);
        // Perform file reading operations
        fileReader.close();
    }
}
```

In the above example, the readFile method throws a checked exception IOException, which is a checked exception related to input/output operations. It must be handled or declared in the method signature.

### Unchecked Exceptions:
Unchecked exceptions, also known as runtime exceptions, do not require explicit handling or declaring in the method signature. They occur due to programming errors or exceptional conditions that can be avoided with proper coding practices. Examples of unchecked exceptions include `NullPointerException`, `ArrayIndexOutOfBoundsException`, and `ArithmeticException`.

Example:
```java
public class Divider {
    public double divide(int dividend, int divisor) {
        return dividend / divisor;
    }
}
```

In the above example, the divide method does not handle or declare any checked exceptions. However, if the divisor parameter is passed as 0, it will throw an unchecked exception `ArithmeticException` at runtime.

It's important to note that unchecked exceptions can still be caught and handled using try-catch blocks, but it's not mandatory.

In summary, checked exceptions need to be explicitly handled or declared, while unchecked exceptions do not require explicit handling. The distinction between checked and unchecked exceptions helps in managing exceptional situations and enforcing proper exception handling practices in Java programs.


### Here are a few more examples of both checked and unchecked exceptions in Java:

### Checked Exceptions:

* FileNotFoundException: Thrown when a file or directory is not found.

* ParseException: Thrown when an error occurs while parsing a string into a specific format.

* InterruptedException: Thrown when a thread is interrupted while it is waiting, sleeping, or otherwise occupied.

* SQLException: Thrown when an error occurs during database access or interaction.

### Unchecked Exceptions:

* NullPointerException: Thrown when a null reference is used where an object is expected.

* ArrayIndexOutOfBoundsException: Thrown when an invalid index is used to access an array.

* ArithmeticException: Thrown when an arithmetic operation encounters an exceptional condition, such as division by zero.

* ClassCastException: Thrown when an invalid type casting operation is performed.

### Here are additional examples of both checked and unchecked exceptions:

### Checked Exceptions:

* IOException: Thrown when an I/O error occurs, such as failure in reading or writing to a file.

* ClassNotFoundException: Thrown when a class is not found at runtime.

* IllegalAccessException: Thrown when access to a class, method, or field is denied.

* InterruptedException: Thrown when a thread is interrupted.

### Unchecked Exceptions:

* IllegalArgumentException: Thrown when an illegal argument is passed to a method. 
* IllegalStateException: Thrown when the state of an object is inappropriate for the requested operation.
* UnsupportedOperationException: Thrown when an unsupported operation is invoked.
* OutOfMemoryError: Thrown when the Java Virtual Machine (JVM) runs out of memory.
* It's important to note that these are just a few examples, and there are many more exceptions available in Java. Additionally, you can also create your own custom exceptions by extending the Exception class or one of its subclasses to handle specific exceptional conditions in your application.

