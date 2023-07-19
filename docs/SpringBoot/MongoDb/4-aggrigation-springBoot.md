---
layout: default
title: Aggregation in SpringBoot
parent: Mongo DB
grand_parent: Spring Boot
nav_order: 5
---
### Aggregation in MongoDB 
Aggregation in MongoDB refers to the process of retrieving and manipulating data from a collection or multiple collections in a structured and organized manner. It allows you to perform complex queries and transformations on your data to extract meaningful insights or create custom reports.

The MongoDB Aggregation Pipeline is the primary mechanism for performing aggregation operations. It consists of a series of stages, where each stage represents a specific operation or transformation applied to the input documents. The output of one stage serves as the input to the next stage, allowing for a chained sequence of operations.

Here are some common stages used in the aggregation pipeline:

1. `$match`: Filters the documents based on specified criteria, similar to the find operation.
2. `$group`: Groups the documents by a specified key and performs aggregation functions such as sum, average, count, etc. on grouped data.
3. `$project`: Selects specific fields or adds new computed fields to the output documents.
4. `$sort`: Sorts the documents based on specified criteria.
5. `$limit` and `$skip`: Limits the number of documents returned or skips a specified number of documents.
6. `$unwind`: Deconstructs an array field from the input documents into multiple documents, creating a separate document for each array element.
7. `$lookup`: Performs a left outer join between two collections based on specified conditions.

These stages, along with others, can be combined in various ways to perform complex aggregations, data transformations, and statistical analysis. Aggregation in MongoDB is powerful and flexible, allowing you to leverage the database's capabilities to derive meaningful insights from your data.

###  Here's a complete Spring Boot example that uses MongoDB with aggregation:
1. Start by setting up your Spring Boot project and adding the necessary dependencies to your `pom.xml` file:
    ```xml
    <!-- MongoDB Starter -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-mongodb</artifactId>
    </dependency>
    ```
2. Create a `Person` entity class representing the collection in MongoDB:
    ```java
    import org.springframework.data.annotation.Id;
    import org.springframework.data.mongodb.core.mapping.Document;
    
    @Document(collection = "Person")
    public class Person {
        @Id
        private String id;
        private String name;
        private int age;
        private String city;
    
        // Constructors, getters, and setters
    }
    ```
3. Create a `PersonAgeStats` class to hold the age statistics:
    ```java
    public class PersonAgeStats {
        private int age;
        private long count;
        private double averageAge;
        private int minAge;
        private int maxAge;
    
        // Constructors, getters, and setters
    }
    ```
4. Create the `PersonRepository` interface that extends `MongoRepository`:
    ```java
    import org.springframework.data.mongodb.repository.MongoRepository;
    
    public interface PersonRepository extends MongoRepository<Person, String> {
    }
    ```
5. Create the `AggregationExampleService` class to handle the aggregation operations:
    ```java
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.data.mongodb.core.MongoTemplate;
    import org.springframework.data.mongodb.core.aggregation.Aggregation;
    import org.springframework.data.mongodb.core.aggregation.AggregationResults;
    import org.springframework.data.mongodb.core.query.Criteria;
    import org.springframework.stereotype.Service;
    
    import java.util.List;
    
    @Service
    public class AggregationExampleService {
    
        private final MongoTemplate mongoTemplate;
    
        @Autowired
        public AggregationExampleService(MongoTemplate mongoTemplate) {
            this.mongoTemplate = mongoTemplate;
        }
    
        public List<PersonAgeStats> getAgeStatsByCity(String city) {
            Criteria criteria = Criteria.where("city").is(city);
            Aggregation aggregation = Aggregation.newAggregation(
                    Aggregation.match(criteria),
                    Aggregation.group("age")
                            .count().as("count")
                            .avg("age").as("averageAge")
                            .min("age").as("minAge")
                            .max("age").as("maxAge")
            );
    
            AggregationResults<PersonAgeStats> results = mongoTemplate.aggregate(aggregation, "Person", PersonAgeStats.class);
            return results.getMappedResults();
        }
    }
    ```
6. Finally, create a controller class to expose the API endpoint:
    ```java
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    
    import java.util.List;
    
    @RestController
    @RequestMapping("/api")
    public class AggregationExampleController {
    
        private final AggregationExampleService aggregationExampleService;
    
        @Autowired
        public AggregationExampleController(AggregationExampleService aggregationExampleService) {
            this.aggregationExampleService = aggregationExampleService;
        }
    
        @GetMapping("/age-stats/{city}")
        public List<PersonAgeStats> getAgeStatsByCity(@PathVariable String city) {
            return aggregationExampleService.getAgeStatsByCity(city);
        }
    }
    ```   
Remember to configure the MongoDB connection details in your `application.properties` file.


