---
layout: default
title: Annotations in Hazelcast
parent: Hazelcast
grand_parent: Spring Boot
nav_order: 5
---
* In Spring Boot with Hazelcast, you can use annotations to configure and customize the behavior of Hazelcast within your application. Here are some of the commonly used annotations in Spring Boot with Hazelcast:

1. `@EnableCaching`: This annotation is used to enable caching support in your Spring Boot application. It allows you to cache method results, thereby improving performance. Hazelcast can be configured as the caching provider using this annotation.
2. `@EnableHazelcastHttpSession`: This annotation enables Hazelcast as the provider for distributed HTTP sessions in your Spring Boot application. It automatically configures Hazelcast's HttpSession integration, allowing session data to be stored in a distributed manner.
3. `@EnableHazelcastRepositories`: This annotation is used to enable Hazelcast as the backend for Spring Data repositories. It scans the specified package(s) for repository interfaces and creates implementations backed by Hazelcast.
4. `@EnableHazelcastCluster`: This annotation is used to enable Hazelcast clustering support in your Spring Boot application. It sets up a Hazelcast cluster by creating and configuring a Hazelcast instance based on the provided configuration.
5. `@HazelcastInstance`: This annotation is used to inject the Hazelcast instance into your Spring Bean. You can use it on a field, setter method, or constructor to automatically inject the Hazelcast instance configured for your application.
6. `@HazelcastAware`: This annotation is used to inject Hazelcast-specific objects into your Spring Bean. It can be used to inject Hazelcast IMap, IQueue, ILock, ITopic, and other Hazelcast data structures or components into your application beans.
7. `@HazelcastPartitionedMap`: This annotation is used to create a Hazelcast Partitioned Map. Partitioned maps can provide high-performance and scalable data storage for large datasets.

These are just a few examples of the annotations used in Spring Boot with Hazelcast. The specific annotations you'll use may depend on your requirements and the functionality you want to achieve with Hazelcast in your application.

### Here's an example of using the `@EnableHazelcastHttpSession` annotation in a Spring Boot application:
`pom.xml`
```xml
<!-- Spring Session with Hazelcast -->
<dependency>
    <groupId>org.springframework.session</groupId>
    <artifactId>spring-session</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.session.config.annotation.web.http.EnableSpringHttpSession;
import org.springframework.session.data.hazelcast.config.annotation.web.http.EnableHazelcastHttpSession;

@SpringBootApplication
@EnableHazelcastHttpSession(maxInactiveIntervalInSeconds = 180) // Set session expiration time to 180 seconds (3 minutes)
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```
In the above example, the `maxInactiveIntervalInSeconds` attribute of the `@EnableHazelcastHttpSession` annotation is set to 180, which means that the session will be invalidated if there is no activity for 3 minutes.

When a session is invalidated due to expiration or when the user manually logs out, Hazelcast will automatically remove the corresponding session data from the distributed session store.

Additionally, you can manually remove session data using Spring Session's `SessionRepository` interface. Here's an example:
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.session.Session;
import org.springframework.session.SessionRepository;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class SessionController {

    @Autowired
    private SessionRepository<? extends Session> sessionRepository;

    @DeleteMapping("/sessions/{sessionId}")
    public void deleteSession(@PathVariable String sessionId) {
        sessionRepository.deleteById(sessionId);
    }
}
```

### Here's an example of using the @EnableHazelcastRepositories annotation in a Spring Boot application:
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.data.hazelcast.repository.config.EnableHazelcastRepositories;

@SpringBootApplication
@EnableHazelcastRepositories(basePackages = "com.example.repository") // Enable Hazelcast as the backend for Spring Data repositories
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```
In the above example, the `@EnableHazelcastRepositories` annotation is used to enable Hazelcast as the backend for Spring Data repositories. It specifies the basePackages attribute, which defines the package(s) where your repository interfaces are located.
`pom.xml`
```xml
<!-- Spring Data with Hazelcast -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```
```java
import org.springframework.data.repository.CrudRepository;

public interface UserRepository extends CrudRepository<User, Long> {
    // Custom query methods and repository operations
}
```
In this example, the `UserRepository` interface extends `CrudRepository` from Spring Data, allowing you to perform CRUD (Create, Read, Update, Delete) operations on the User entity.

Spring Data will handle the implementation details, leveraging Hazelcast as the storage backend for these repositories. You can then inject and use the repository in your services or controllers to interact with the underlying data store.

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    // Getters and setters
}
```
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserRepository userRepository;

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userRepository.findById(id)
                .orElseThrow(() -> new NotFoundException("User not found with id: " + id));
    }

    // Other CRUD operations and custom queries
}
```

### Here's a complete example of using the `@EnableHazelcastCluster` annotation in a Spring Boot application to enable Hazelcast clustering:
`pom.xml`
```xml
<!-- Hazelcast -->
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```
Next, create a Hazelcast configuration file named `hazelcast.xml` in the `src/main/resources` directory with the desired configuration. For example:
```xml
<hazelcast xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.hazelcast.com/schema/config
           http://www.hazelcast.com/schema/config/hazelcast-config-4.2.xsd">

    <network>
        <join>
            <multicast enabled="false"/>
            <tcp-ip enabled="true">
                <member>127.0.0.1</member> <!-- Replace with actual IP addresses of cluster members -->
            </tcp-ip>
        </join>
    </network>

</hazelcast>
```
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;
import com.hazelcast.config.Config;
import com.hazelcast.config.FileSystemXmlConfig;

@SpringBootApplication
@EnableCaching
@EnableHazelcastCluster
public class MyApp {
    public static void main(String[] args) {
        Config config = new FileSystemXmlConfig("src/main/resources/hazelcast.xml");
        SpringApplication.run(MyApp.class, args);
    }
}
```
In this example, the `@EnableHazelcastCluster` annotation enables Hazelcast clustering in the Spring Boot application. The Config object is created using the `hazelcast.xml` configuration file.

Note that in a real-world scenario, you may need to adjust the network configuration in the hazelcast.xml file based on your deployment environment. Replace the <member> element with the actual IP addresses or hostnames of the cluster members.

Now you can use Hazelcast features, such as caching and distributed data structures, in your application. You can also leverage Spring's caching annotations (`@Cacheable`, `@CachePut`, etc.) along with Hazelcast to cache method results.

### Here's a complete example of using the `@HazelcastInstance` annotation in a Spring Boot application to inject the Hazelcast instance:
`pom.xml`
```xml
<!-- Hazelcast -->
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```
```java
import com.hazelcast.core.IMap;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import com.hazelcast.core.HazelcastInstance;

@SpringBootApplication
public class MyApp {
    @Autowired
    private HazelcastInstance hazelcastInstance;

    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }

    public void useHazelcastInstance() {
        IMap<String, Integer> map = hazelcastInstance.getMap("my-distributed-map");
        map.put("key", 42);
        Integer value = map.get("key");
        System.out.println("Value: " + value);
    }
}
```

### `@HazelcastAware` and `@HazelcastPartitionedMap`
The `@HazelcastAware` and `@HazelcastPartitionedMap` annotations are not built-in annotations provided by Spring Boot or Hazelcast. However, I can provide you with an example of a custom implementation of these annotations using Hazelcast in a Spring Boot application.
```java
import org.springframework.beans.factory.annotation.Autowired;

import java.lang.annotation.*;

@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@Autowired
public @interface HazelcastAware {
}
```

```java
import java.lang.annotation.*;

@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface HazelcastPartitionedMap {
    String name() default "";
}
```
```java
import com.hazelcast.core.HazelcastInstance;
import com.hazelcast.core.IMap;
import org.springframework.beans.factory.annotation.Autowired;

public class MyService {

    @HazelcastAware
    private HazelcastInstance hazelcastInstance;

    @HazelcastPartitionedMap(name = "myPartitionedMap")
    private IMap<String, String> partitionedMap;

    // Use the injected Hazelcast objects in your application
    // ...
}
```
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class MyApp {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(MyApp.class, args);
        MyService myService = context.getBean(MyService.class);
        // Use the myService instance
    }
}
```
Note: Since the `@HazelcastAware` and `@HazelcastPartitionedMap` annotations are custom annotations, you would need to handle the logic for injecting the Hazelcast objects and managing partitioned maps manually, potentially using Hazelcast's APIs and configurations within the custom annotations.



