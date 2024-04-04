---
layout: default
title: Neo4j Health check
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 3
---
# Neo4j Health check

```java
@Configuration
public class Neo4jHealthIndicator extends AbstractHealthIndicator {
    @Autowired
    Neo4jService neo4jService;

    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        List<Record> statement = neo4jService.runStatement("CALL dbms.queryJmx('org.neo4j:*')", null);
        if (statement != null && statement.size() > 0) {
            builder.up();
        } else {
            builder.down();
        }
    }
}
```
You need to implement `Neo4jService` to communicate with Neo4j database. This can be covered in the separate post. 
`AbstractHealthIndicator` can found in the Spring Actuator library 

### Using Spring reactor
```java
@Component
public class Neo4jHealthIndicator implements ReactiveHealthIndicator {
    private final Neo4jService neo4jService;

    public Neo4jHealthIndicator(Neo4jService neo4jService) {
        this.neo4jService = neo4jService;
    }

    @Override
    public Mono<Health> health() {
        return Mono.fromSupplier(() -> neo4jService.runStatement("CALL dbms.queryJmx('org.neo4j:*')", null))
                .flatMap(statement -> {
                    if (statement != null && statement.size() > 0) {
                        return Mono.just(Health.up().build());
                    } else {
                        return Mono.just(Health.down().build());
                    }
                }).onErrorResume(e -> Mono.just(Health.down().withException(e).build()));
    }
}
```

### Mono.fromSupplier
`Mono.fromSupplier` is a factory method in the Reactor framework used to create a Mono from a `java.util.function.Supplier`. It allows you to lazily produce a single item that will be emitted by the returned Mono when subscribed to.

The Supplier is a functional interface that can be implemented to provide a value. The `Mono.fromSupplier` method takes a Supplier as an argument and returns a Mono that, when subscribed to, will call the Supplier to produce a value. The value produced by the Supplier is then emitted as the single item in the reactive stream.

In the code snippet, the `Mono.fromSupplier` method is used to wrap the result of the call to `neo4jService.runStatement` in a Mono. This allows the result of the call to be transformed using the `flatMap` method.


```java
@Configuration
public class Neo4jHealthIndicator extends ReactiveHealthIndicator {
    
    private final Neo4jService neo4jService;
    
    public Neo4jHealthIndicator(Neo4jService neo4jService) {
        this.neo4jService = neo4jService;
    }
    
    @Override
    public Mono<Health> health() {
        return Mono.defer(() -> {
            return neo4jService.runStatement("CALL dbms.queryJmx('org.neo4j:*')", null)
                    .flatMap(statement -> {
                        if (statement != null && statement.size() > 0) {
                            return Health.up().build();
                        } else {
                            return Health.down().build();
                        }
                    });
        });
    }
}
```

### Mono.defer
`Mono.defer` is a factory method in the Reactor framework used to delay the creation of a Mono until it is subscribed to. When a Mono created with `Mono.defer` is subscribed to, the function passed to `Mono.defer` is executed and its result is used to produce the Mono. This allows for creating a new Mono every time it is subscribed to, ensuring that its behavior is up-to-date.

### Difference between Mono.fromSupplier and Mono.defer
`Mono.fromSupplier` and Mono.defer are both factory methods used to create a Mono in the Reactor framework. The main difference between them is when the supplier passed to `Mono.fromSupplier` is executed and when the deferred computation passed to `Mono.defer` is executed.

`Mono.fromSupplier` executes the supplier immediately when the Mono is created, while `Mono.defer` delays the execution of the deferred computation until the Mono is subscribed to.

In other words, `Mono.fromSupplier` executes the supplier as soon as the Mono is created, whereas `Mono.defer` executes the deferred computation each time the Mono is subscribed to. This allows `Mono.defer` to produce up-to-date values each time it is subscribed to.

In the code snippet, `Mono.defer` was used because the behavior of the health check needs to be updated each time it is executed. Using `Mono.fromSupplier` would have resulted in the same value being emitted each time the Mono is subscribed to, which would not reflect the current state of the health check.

#### Sample Rest controller
```java
@RestController
public class AdminController {
    private static final Logger LOGGER = LoggerFactory.getLogger(AdminController.class);

    @GetMapping(value = "/health")
    public Mono<ResponseEntity<Void>> getHealth() {
        LOGGER.info("AdminController: health api called!");
        return Mono.just(new ResponseEntity<>(HttpStatus.OK));
    }
}
```

```java
@RestController
public class AdminController {

    private static final Logger LOGGER = LoggerFactory.getLogger(AdminController.class);

    @GetMapping(value = "/health")
    public ResponseEntity<Void> getHealth(){
        LOGGER.info("AdminController: health api called!");
        return new ResponseEntity<>(HttpStatus.OK);
    }
}
```
