
# Thread in Java

In Java, a thread is a lightweight unit of execution that allows concurrent execution of code within a program. It represents a single sequential flow of control within a program.

Threads in Java are created by either extending the Thread class or implementing the Runnable interface. Here are the two approaches:

### 1. Extending the Thread class:

* Create a new class that extends the `Thread` class.
* Override the `run(`)` method in the new class to define the code that will run concurrently.
* Create an instance of the new class.
* Call the `start()` method on the instance to start the execution of the thread.

### Example:
```java
public class MyThread extends Thread {
    public void run() {
        // Code to be executed concurrently
    }
}

// Creating and starting a new thread
MyThread thread = new MyThread();
thread.start();
```
2. Implementing the Runnable interface:

* Create a new class that implements the Runnable interface.
* Implement the run() method defined by the Runnable interface with the code that will run concurrently.
* Create an instance of the new class.
* Create a new Thread instance, passing the instance of the class implementing Runnable as a parameter to the Thread constructor.
* Call the start() method on the Thread instance to start the execution of the thread.

### Example:
```java
public class MyRunnable implements Runnable {
    public void run() {
        // Code to be executed concurrently
    }
}

// Creating and starting a new thread
MyRunnable myRunnable = new MyRunnable();
Thread thread = new Thread(myRunnable);
thread.start();
```

Both approaches allow you to execute code concurrently within your program. Using threads can be beneficial when you want to perform tasks simultaneously or handle tasks that may block, such as network operations or time-consuming computations, without blocking the main execution flow of the program.

Certainly! Here's a complete example that demonstrates creating and running a thread using both approaches:

Approach 1: Extending the `Thread` class
```java
public class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread: " + i);
            try {
                Thread.sleep(500); // Sleep for 500 milliseconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();
        
        for (int i = 1; i <= 5; i++) {
            System.out.println("Main Thread: " + i);
            try {
                Thread.sleep(500); // Sleep for 500 milliseconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

Approach 2: Implementing the Runnable interface
```java
public class MyRunnable implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread: " + i);
            try {
                Thread.sleep(500); // Sleep for 500 milliseconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread thread = new Thread(myRunnable);
        thread.start();

        for (int i = 1; i <= 5; i++) {
            System.out.println("Main Thread: " + i);
            try {
                Thread.sleep(500); // Sleep for 500 milliseconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### Differences

The main difference between using the Thread class and implementing the Runnable interface lies in the class hierarchy and flexibility.

### Using the Thread class:

* By extending the Thread class, your class becomes a subclass of Thread, and you can directly override the run() method to define the code that will run concurrently.
* This approach is suitable when your class needs to have additional thread-related functionality or when you want to customize the behavior of the Thread class itself.
* However, it limits your class's ability to extend other classes since Java does not support multiple inheritance. If your class already extends another class, using the Runnable interface is a more flexible option.

#### Implementing the Runnable interface:

* By implementing the Runnable interface, your class can still define the code that will run concurrently by implementing the run() method, but it does not become a thread itself.
* This approach is suitable when you want your class to be more flexible and share the same instance with multiple threads or reuse the same instance with different Thread objects.
* It allows your class to extend another class or implement other interfaces, providing more flexibility and avoiding the limitation of single inheritance.
* Additionally, using the Runnable interface separates the task (the run() method) from the thread (the Thread instance), promoting a separation of concerns.

#### Here are some use cases for each approach:

### Using the `Thread` class:

* You want to customize or extend the functionality of the Thread class itself.
* You have a specific need for thread-related methods or properties provided by the Thread class.
* You don't need to extend any other class or can work around the limitation of single inheritance.

### Using the Runnable interface:

* You want your class to be more flexible and reusable by implementing multiple interfaces or extending another class.
* You want to separate the task logic from the thread logic to promote a separation of concerns.
* You want to share the same task implementation among multiple threads or reuse the same task implementation with different Thread objects.

In general, using the Runnable interface is often recommended due to its flexibility and better support for object-oriented design principles. It allows for better code organization and reuse, especially when dealing with complex systems or multi-threaded applications.

### ---
In Java, a thread is an independent unit of execution, and it does not have a return value like a regular method. Once a thread starts executing, it continues until the run() method completes or an uncaught exception is thrown.

However, there are a few ways to obtain a result or communicate information from a thread to the rest of the program:

1. Instance Variables: You can define instance variables within the class that extends Thread or implements `Runnable` and use them to store the result or any other information you need. Other parts of the program can access these variables after the thread has completed its execution.

2. Shared Data Structures: You can use shared data structures, such as `ArrayList`, `Queue`, or `Map`, to exchange data between threads. Synchronization mechanisms, like locks or concurrent collections, can be used to ensure thread-safe access to these shared data structures.

3. `Callbacks` or `Listener` Interfaces: You can define callback methods or listener interfaces that are invoked by the thread when it completes its execution or reaches a specific state. Other parts of the program can register callbacks or listeners and receive the result or relevant information when the thread finishes.

4. CompletableFuture (Java 8+): The CompletableFuture class provides a powerful mechanism to handle asynchronous computations and obtain results from them. It allows you to chain multiple operations, handle exceptions, and wait for the completion of the computation.

Here's a simplified example using CompletableFuture to demonstrate how you can obtain a result from a thread:

```java
import java.util.concurrent.*;

public class MyThread implements Callable<String> {
    public String call() {
        // Perform some computation
        String result = "Thread execution completed";
        return result;
    }

    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<String> future = executor.submit(new MyThread());

        // Perform other tasks while the thread is executing

        String result = future.get(); // Blocks until the thread completes and returns the result
        System.out.println(result);

        executor.shutdown();
    }
}
```
In this example, the `MyThread` class implements the `Callable` interface and overrides the `call()` method, which performs some computation and returns a result. The `ExecutorService` is used to submit the task as a `Callable` and obtain a `Future` object. The `get()` method is then called on the `Future` object to retrieve the result.

### Interprocess communication (IPC)
In Java, interprocess communication (IPC) can be achieved using various mechanisms. Here are a few commonly used methods for IPC in Java:

### Socket Programming:

* TCP/IP or UDP sockets can be used to establish communication between processes running on different machines or on the same machine.
* The java.net package provides classes like Socket and ServerSocket for TCP/IP communication, and DatagramSocket and DatagramPacket for UDP communication.
* Sockets allow bidirectional communication by exchanging data through input and output streams.

### Java RMI (Remote Method Invocation):

* Java RMI enables communication between processes running on different JVMs (Java Virtual Machines).
* It allows you to invoke methods on remote objects as if they were local objects.
* RMI uses Java interfaces and the java.rmi package to define remote objects and their methods.

### Java Messaging Service (JMS):

* JMS is a Java API for asynchronous messaging between applications.
* It provides a way for different processes to exchange messages through message queues or topics.
* JMS implementations, like Apache ActiveMQ or RabbitMQ, can be used for messaging between Java processes.

### Shared Memory:

* Shared memory allows processes to communicate by accessing shared regions of memory.
* In Java, you can use the java.nio package to create shared memory regions and use byte buffers to read and write data.
* Libraries like Java Native Access (JNA) or Java Native Interface (JNI) can be used to interact with native code and access shared memory.

### File-Based Communication:

* Processes can communicate by reading and writing to shared files.
* One process writes data to a file, and the other process periodically checks the file for new data.
* Proper synchronization mechanisms, like locks or signaling, should be used to ensure data integrity and avoid conflicts.

### Remote Procedure Calls (RPC):

* RPC allows processes to call procedures or functions on remote systems.
* Libraries like Apache Thrift or gRPC provide RPC frameworks that support communication between different programming languages.
* These are some of the common methods for interprocess communication in Java. The choice of method depends on factors such as the nature of communication, the network environment, the desired level of abstraction, and the specific requirements of the application.

### How to communicate between threads 
In Java, there are several ways to communicate between threads. Here are some common mechanisms:

### Shared Objects:

* Threads can communicate by accessing and modifying shared objects in memory.
* The shared objects can be regular objects or data structures like ArrayList, Queue, or Map.
* Proper synchronization mechanisms, such as locks or synchronized blocks, should be used to ensure thread-safe access to shared objects and prevent data races or inconsistencies.

### Wait and Notify:

* The wait() and notify() methods provided by the Object class can be used for thread synchronization and communication.
* Threads can wait for a condition using the wait() method, and other threads can notify them when the condition is met using the notify() or notifyAll() methods.
* This mechanism allows threads to coordinate and communicate by signaling each other.

### Blocking Queues:

* Java's BlockingQueue interface and its implementations, like ArrayBlockingQueue or LinkedBlockingQueue, provide a thread-safe way to pass data between threads.
* One thread can put an item into the queue using the put() or offer() methods, and another thread can take items from the queue using the take() or poll() methods.
* Blocking queues handle the synchronization and blocking operations internally, making it easier to implement producer-consumer scenarios or thread pools.

### CountDownLatch and CyclicBarrier:

* The CountDownLatch and CyclicBarrier classes from the java.util.concurrent package can be used for synchronization and coordination between threads.
* A CountDownLatch allows one or more threads to wait until a specified number of operations or events complete.
* A CyclicBarrier allows a set of threads to wait until all threads reach a barrier point before continuing.

### Thread Signaling:

* Threads can use shared boolean flags or variables to signal each other.
* One thread can set a flag or update a variable, and other threads can check the flag or variable periodically to respond accordingly.
* Care should be taken to ensure proper synchronization and visibility of shared variables to avoid race conditions or stale data.
* These are some of the common mechanisms for thread communication in Java. The choice of mechanism depends on the specific requirements of the application and the type of communication needed between the threads. It's important to ensure proper synchronization and thread safety to avoid data inconsistencies and race conditions.

### Difference between `Callable` and `Runnable`
In Java, both Callable and Runnable are interfaces that are commonly used to define tasks or actions that can be executed concurrently. The main difference between them lies in the return value and the ability to throw exceptions. Here are the key distinctions:

1. Return Value:

* `Runnable` does not have a return value. The `run()` method in the `Runnable` interface has a void return type, meaning it does not return a value.
* `Callable` defines a `call()` method that returns a value. The `call()` method has a generic return type (<V>) and returns an object of that type.

2. Exception Throwing:

* `Runnable` cannot throw checked exceptions directly. The `run()` method of `Runnable` does not declare any checked exceptions.
* `Callable` can throw checked exceptions. The `call()` method of Callable can declare checked exceptions that need to be handled or propagated.

3. Usage with `Executors`:

* `Runnable` is commonly used with the `Executor` framework (`ExecutorService`, `ThreadPoolExecutor`) to submit tasks for execution.
* `Callable` is also used with the `Executor` framework, but it is specifically designed for returning a value or throwing exceptions. It is often used when you need to execute a task and obtain a result.

### Here's a simple code example to illustrate the usage of `Runnable` and `Callable`:
```java
import java.util.concurrent.*;

public class RunnableVsCallable {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        Runnable runnableTask = () -> {
            System.out.println("Runnable task executed");
        };

        Callable<String> callableTask = () -> {
            System.out.println("Callable task executed");
            return "Callable result";
        };

        ExecutorService executor = Executors.newSingleThreadExecutor();

        // Execute the Runnable task
        executor.execute(runnableTask);

        // Execute the Callable task and obtain the result
        Future<String> future = executor.submit(callableTask);
        String result = future.get();
        System.out.println("Callable result: " + result);

        executor.shutdown();
    }
}
```
### `Executors`  and `ExecutorService`
In Java, the Executors class and ExecutorService interface are part of the concurrency utility framework, which provides a higher-level abstraction for managing and executing concurrent tasks. They simplify the process of creating and managing threads in a concurrent application.

### Executors:

* The Executors class provides factory methods for creating different types of ExecutorService instances.

* It offers static methods to create thread pools with fixed or variable numbers of threads, single-threaded executors, or cached thread pools.

* Thread pools created by the Executors class manage the execution of tasks and provide features like thread reuse, scheduling, and task queuing.

### `ExecutorService`:

* The `ExecutorService` interface extends the `Executor` interface and provides additional functionality.

* It represents an asynchronous execution service that manages the execution of tasks submitted via the `execute()` or `submit()` methods.

* The `ExecutorService` provides methods to submit tasks, control their execution, and obtain Future objects for monitoring task progress and obtaining results.

* It also provides methods for shutting down the executor gracefully, allowing running tasks to complete while rejecting new tasks.

### Here's an example that demonstrates the usage of Executors and ExecutorService to execute tasks concurrently:
```java
import java.util.concurrent.*;

public class ExecutorExample {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(3);

        for (int i = 0; i < 5; i++) {
            Runnable task = () -> {
                String threadName = Thread.currentThread().getName();
                System.out.println("Task executed by " + threadName);
            };
            executorService.execute(task);
        }

        executorService.shutdown();
    }
}
```
In this example, a fixed thread pool with three threads is created using `Executors.newFixedThreadPool(3)`. Five tasks, defined as `Runnable` instances, are submitted to the executor service using the `execute()` method. The executor service manages the execution of these tasks concurrently among the available threads in the thread pool. Finally, the `shutdown()` method is called to gracefully shut down the executor service.

Using `ExecutorService` instead of managing threads manually provides benefits such as thread reuse, thread pool management, and task scheduling. It abstracts away the complexities of managing threads, improves code organization, and helps in building scalable and efficient concurrent applications.

### CompletableFuture
`CompletableFuture` is a class introduced in Java 8 as part of the `java.util.concurrent` package. It represents a promise or future result of an asynchronous computation. It provides a powerful and flexible way to handle asynchronous tasks and their results.

Here are some key features and functionalities of `CompletableFuture`:

### Asynchronous Execution:

* `CompletableFuture` supports asynchronous execution of tasks.

* Tasks can be executed asynchronously using methods like `runAsync()` and `supplyAsync()`.

* Asynchronous tasks are executed in separate threads, allowing the calling thread to continue with other operations.

### Chaining and Composition:

* `CompletableFuture` supports chaining and composition of multiple tasks.

* Tasks can be combined using methods like `thenApply()`, `thenAccept()`, and `thenCompose()`.

* Chained tasks can depend on the result of previous tasks, allowing for complex workflows and dependencies.

### Exception Handling:

* `CompletableFuture` provides mechanisms for handling exceptions that occur during task execution.

* `Exceptions` can be handled using methods like `exceptionally()` and `handle()`.

* Exceptional results can be propagated through the chain of `CompletableFuture` instances.

### Waiting for Completion and Obtaining Results:

* `CompletableFuture` allows you to wait for the completion of asynchronous tasks and obtain their results.

* You can use methods like `get()` or `join()` to block and wait for the result.

* `CompletableFuture` also supports timeouts and cancellation of tasks.

### Combining Multiple Results:

* `CompletableFuture` provides methods for combining the results of multiple tasks.
* You can use methods like `thenCombine()`, `thenAcceptBoth()`, or `allOf()` to combine and process results from multiple `CompletableFuture` instances.

### Integration with Concurrency Framework:

* `CompletableFuture` integrates well with other components of the concurrency framework, such as `ExecutorService`.

* You can specify an executor for executing the asynchronous tasks using methods like `runAsync()` and `supplyAsync()`.

* Here's a simplified example that demonstrates the usage of `CompletableFuture`:

```java
import java.util.concurrent.*;

public class CompletableFutureExample {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> "Hello")
                .thenApplyAsync(result -> result + " World")
                .thenApplyAsync(String::toUpperCase);

        String finalResult = future.get();
        System.out.println(finalResult);
    }
}
```
In this example, a `CompletableFuture` is created using the `supplyAsync()` method, which asynchronously executes a task that supplies the initial string "Hello". Then, two transformations (`thenApplyAsync()`) are chained to the future, where the string is appended with " World" and converted to uppercase. Finally, the result is obtained using the `get()` method.

`CompletableFuture` provides many more methods and functionalities, allowing you to handle complex asynchronous tasks and their results with ease. It is a powerful tool for writing concurrent and asynchronous code in Java.




