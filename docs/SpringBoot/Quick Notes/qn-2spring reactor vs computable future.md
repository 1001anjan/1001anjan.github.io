---
layout: default
title: Spring reactor vs computable future
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 2
---
# Spring reactor vs computable future
Spring Reactor and Computable Futures are both reactive programming frameworks.

Spring Reactor is part of the Spring framework, a Java-based framework for building web applications. Reactor provides a reactive programming model for building applications that are responsive, resilient, and scalable. It integrates with the Spring ecosystem and provides a foundation for building reactive applications with the Spring framework.

Computable Futures is a Java library for building asynchronous and non-blocking applications using Java's CompletableFuture API. It provides a set of convenient utility methods for working with CompletableFuture objects and supports functional composition and error handling.

In summary, both frameworks provide support for reactive programming, but Spring Reactor is more focused on integration with the Spring framework while Computable Futures focuses on utilizing the CompletableFuture API.


#### Choices
The best choice between Spring Reactor and Computable Futures depends on the specific needs of a project.

If you are building a Java-based web application and want to use a reactive programming model, Spring Reactor is a good choice as it is integrated with the Spring framework and provides a comprehensive solution for building reactive applications.

If you want to use the CompletableFuture API for building asynchronous and non-blocking applications, Computable Futures might be a better choice. It provides a set of convenient utility methods for working with CompletableFuture objects, and supports functional composition and error handling.

Ultimately, the best choice depends on the requirements of your specific project, so it's important to consider the features, benefits, and limitations of both frameworks before making a decision.

### Some use cases for Spring Reactor and Computable Futures are:

Spring Reactor:

* Building web applications that need to handle high levels of concurrency and handle a large number of requests efficiently.
* Applications that need to process and aggregate data from multiple sources in real-time.
* Building microservices architecture and reactive systems.

Computable Futures:

* Applications that need to perform multiple independent operations in parallel and want to process the results as soon as they become available.
* Applications that need to perform long-running operations asynchronously to improve responsiveness.
* Applications that need to handle errors and exceptions during the execution of asynchronous operations.

Note: These are just examples and there may be other use cases that are better suited to a specific framework. It's important to consider the specific requirements of a project before deciding which framework to use.