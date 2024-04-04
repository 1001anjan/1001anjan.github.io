---
layout: default
title: Spring Reactor WebClient
parent: Spring Reactor
grand_parent: Spring Boot
nav_order: 5
---
# Spring Reactor WebClient
Here's an example of how you can use the Spring Reactor `WebClient` to perform an HTTP GET request:

```java
@RestController
public class ExampleController {

    private final WebClient webClient = WebClient.create("https://jsonplaceholder.typicode.com");

    @GetMapping("/example")
    public Mono<String> example() {
        return webClient.get()
                        .uri("/posts/1")
                        .retrieve()
                        .bodyToMono(Map.class)
                        .map(m -> (String) m.get("title"))
                        .onErrorResume(e -> Mono.just("Error Occurred"));
    }
}
```

Here's an example of how you could create a `WebClient` bean in Spring Boot and reuse it in multiple controllers:

```java
@Configuration
public class WebClientConfig {

    @Bean
    public WebClient webClient() {
        return WebClient.create("https://jsonplaceholder.typicode.com");
    }
}

@RestController
public class ExampleController1 {

    private final WebClient webClient;

    public ExampleController1(WebClient webClient) {
        this.webClient = webClient;
    }

    @GetMapping("/example1")
    public Mono<String> example1() {
        return webClient.get()
                        .uri("/posts/1")
                        .retrieve()
                        .bodyToMono(Map.class)
                        .map(m -> (String) m.get("title"))
                        .onErrorResume(e -> Mono.just("Error Occurred"));
    }
}

@RestController
public class ExampleController2 {

    private final WebClient webClient;

    public ExampleController2(WebClient webClient) {
        this.webClient = webClient;
    }

    @GetMapping("/example2")
    public Mono<String> example2() {
        return webClient.get()
                        .uri("/posts/2")
                        .retrieve()
                        .bodyToMono(Map.class)
                        .map(m -> (String) m.get("title"))
                        .onErrorResume(e -> Mono.just("Error Occurred"));
    }
}
```

### Here's an example of how you could handle different response codes using Spring Boot's `WebClient`:
```java
@RestController
public class ExampleController {

    private final WebClient webClient;

    public ExampleController(WebClient webClient) {
        this.webClient = webClient;
    }

    @GetMapping("/example")
    public Mono<String> example() {
        return webClient.get()
                        .uri("/posts/1")
                        .retrieve()
                        .onStatus(HttpStatus::is4xxClientError, response -> Mono.just("Bad Request"))
                        .onStatus(HttpStatus::is5xxServerError, response -> Mono.just("Server Error"))
                        .bodyToMono(Map.class)
                        .map(m -> (String) m.get("title"))
                        .onErrorResume(e -> Mono.just("Error Occurred"));
    }
}
```
### Sending `ResponseEntity`
```java
@RestController
public class ExampleController {

    private final WebClient webClient;

    public ExampleController(WebClient webClient) {
        this.webClient = webClient;
    }

    @GetMapping("/example")
    public Mono<ResponseEntity<String>> example() {
        return webClient.get()
                        .uri("/posts/1")
                        .retrieve()
                        .onStatus(HttpStatus::is4xxClientError, response -> Mono.just(ResponseEntity.badRequest().body("Bad Request")))
                        .onStatus(HttpStatus::is5xxServerError, response -> Mono.just(ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Server Error")))
                        .bodyToMono(Map.class)
                        .map(m -> (String) m.get("title"))
                        .map(title -> ResponseEntity.ok(title))
                        .onErrorResume(e -> Mono.just(ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Error Occurred")));
    }
}
```
### Here is an example of using `.retry` in Spring Boot with a `WebClient` to call a REST API:

```java
@Service
public class RetryExampleService {

    private final WebClient webClient;

    public RetryExampleService(WebClient.Builder webClientBuilder) {
        this.webClient = webClientBuilder.baseUrl("https://api.example.com").build();
    }

    public Mono<Response> retryGetRequest(String path) {
        return webClient.get().uri(path)
                .retrieve()
                .onStatus(HttpStatus::is5xxServerError, response -> Mono.error(new RetryableException("Error")))
                .bodyToMono(Response.class)
                .retryWhen(Retry.backoff(3, Duration.ofSeconds(2)));
    }
}

@RestController
@RequestMapping("/retry")
public class RetryExampleController {

    private final RetryExampleService service;

    public RetryExampleController(RetryExampleService service) {
        this.service = service;
    }

    @GetMapping("/{path}")
    public Mono<Response> getData(@PathVariable String path) {
        return service.retryGetRequest(path);
    }
}
```

### Here is an example of how to return an error when a `timeout` occurs in a `WebClient` in Spring Boot:
```java
@Service
public class TimeoutExampleService {

    private final WebClient webClient;

    public TimeoutExampleService(WebClient.Builder webClientBuilder) {
        this.webClient = webClientBuilder.baseUrl("https://api.example.com").build();
    }

    public Mono<Response> getDataWithTimeout(String path) {
        return webClient.get().uri(path)
                .retrieve()
                .bodyToMono(Response.class)
                .timeout(Duration.ofSeconds(5), Mono.error(new TimeoutException("Timeout occurred")));
    }
}

@RestController
@RequestMapping("/timeout")
public class TimeoutExampleController {

    private final TimeoutExampleService service;

    public TimeoutExampleController(TimeoutExampleService service) {
        this.service = service;
    }

    @GetMapping("/{path}")
    public Mono<Response> getData(@PathVariable String path) {
        return service.getDataWithTimeout(path);
    }
}
```



