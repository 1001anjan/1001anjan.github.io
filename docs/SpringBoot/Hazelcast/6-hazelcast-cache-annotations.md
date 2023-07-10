---
layout: default
title: Cache Annotations in Hazelcast
parent: Hazelcast
grand_parent: Spring Boot
nav_order: 6
---
### Here are the annotations provided by Hazelcast for handling caching:

* `@Cacheable`: This annotation is used to indicate that a method's result should be cached. When a method annotated with @Cacheable is invoked, Hazelcast checks if the cache already contains the requested data. If it does, the cached result is returned instead of executing the method.
* `@CachePut`: This annotation is used to update the cache with the result of a method invocation. When a method annotated with @CachePut is invoked, Hazelcast updates the cache with the method's return value, regardless of whether the cache already contains an entry for the given key.
* `@CacheEvict`: This annotation is used to remove entries from the cache. When a method annotated with @CacheEvict is invoked, Hazelcast removes the corresponding entry from the cache. This annotation supports various options for cache eviction, such as evicting a specific entry, all entries in a cache, or entries based on certain conditions.
* `@Caching`: This annotation is used to apply multiple cache-related annotations to a single method. With @Caching, you can combine multiple caching annotations like @Cacheable, @CachePut, and @CacheEvict to define complex caching behavior for a method.

### Here's an example that demonstrates the usage of Hazelcast caching annotations in a Spring Boot application with MongoDB as the data store.
`pom.xml`
```xml
<!-- Spring Boot Starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>

<!-- Spring Data MongoDB -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>

<!-- Hazelcast Integration -->
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```
```java
@SpringBootApplication
@EnableCaching
public class HazelcastCacheExampleApplication {

    public static void main(String[] args) {
        SpringApplication.run(HazelcastCacheExampleApplication.class, args);
    }

}
```
```java
@Document(collection = "persons")
public class Person {

    @Id
    private String id;
    private String name;
    private int age;

    // Constructors, getters, setters
}
```
```java
public interface PersonRepository extends MongoRepository<Person, String> {

    @Cacheable("persons")
    Person findByName(String name);

    @CachePut(value = "persons", key = "#person.name")
    Person save(Person person);

    @CacheEvict(value = "persons", allEntries = true)
    void deleteAll();

}
```
In the repository interface, we have used the Hazelcast caching annotations:
* `@Cacheable`: Caches the result of the findByName method based on the name parameter.
* `@CachePut`: Updates the cache with the saved Person object. The cache key is derived from the name property of the Person object.
* `@CacheEvict`: Clears the entire cache when the deleteAll method is invoked.

```java
@Service
public class PersonService {

    private final PersonRepository personRepository;

    public PersonService(PersonRepository personRepository) {
        this.personRepository = personRepository;
    }

    public Person findPersonByName(String name) {
        return personRepository.findByName(name);
    }

    public Person savePerson(Person person) {
        return personRepository.save(person);
    }

    public void deleteAllPersons() {
        personRepository.deleteAll();
    }
}
```