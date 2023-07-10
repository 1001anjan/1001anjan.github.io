---
layout: default
title: Hazelcast with Database
parent: Hazelcast
grand_parent: Spring Boot
nav_order: 3
---
### Here's an example of a Spring Boot application that uses Hazelcast for distributed caching and PostgreSQL as the database:
`pom.xml`
```xml
<dependencies>
    <!-- Spring Boot dependencies -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    
    <!-- Hazelcast dependencies -->
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast</artifactId>
    </dependency>
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast-spring</artifactId>
    </dependency>
    
    <!-- PostgreSQL dependency -->
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
    </dependency>
</dependencies>
```
`application.properties`
```yml
# Hazelcast configuration
hazelcast.config=classpath:hazelcast.xml

# PostgreSQL configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/mydatabase
spring.datasource.username=dbuser
spring.datasource.password=dbpassword
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
```
Create a `hazelcast.xml` file in the `src/main/resources` directory to define the Hazelcast configuration:
```xml
<hazelcast xsi:schemaLocation="http://www.hazelcast.com/schema/config hazelcast-config-3.12.xsd"
           xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <group>
        <name>myHazelcastCluster</name>
        <password>myHazelcastPassword</password>
    </group>

    <network>
        <port auto-increment="true">5701</port>
        <join>
            <multicast enabled="false"/>
            <tcp-ip enabled="true">
                <member>localhost</member>
            </tcp-ip>
        </join>
    </network>

    <map name="myCache">
        <time-to-live-seconds>3600</time-to-live-seconds>
        <max-idle-seconds>1800</max-idle-seconds>
        <eviction-policy>LRU</eviction-policy>
        <max-size policy="PER_NODE">10000</max-size>
    </map>
</hazelcast>
```
`User.java`
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
    private String email;
    
    // Getters and setters
    
    // ...
}
```
`UserRepository.java`
```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // Add custom query methods if needed
    void deleteById(Long id);
}
```
`UserService.java`
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    @Cacheable("myCache")
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    @CacheEvict(value = "myCache", key = "#id")
    public void deleteUser(Long id) {
        userRepository.deleteById(id);
    }
}
```
`UserController.java`
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserService userService;

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
    }
}
```