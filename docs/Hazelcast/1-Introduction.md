---
layout: default
title: Hazelcast Introduction
parent: Hazelcast
nav_order: 1
---
### Hazelcast [Official Link](https://docs.hazelcast.com/hazelcast/5.3/)
Hazelcast is an open-source, in-memory data grid (IMDG) and stream processing platform. It provides a distributed computing solution for processing large amounts of data across multiple nodes and allows for high-performance and low-latency data access.

Here are some key features and concepts related to Hazelcast:

1. In-Memory Data Grid (IMDG): Hazelcast stores data in memory across a cluster of nodes, providing fast and efficient access to data. It distributes data across nodes using a partitioning scheme and provides automatic data replication for fault tolerance.

2. Distributed Computing: Hazelcast enables distributed computing by allowing you to execute operations on the data stored in the IMDG in parallel across the cluster. It supports distributed data structures like maps, queues, lists, sets, and more, which can be accessed and manipulated in a distributed manner.

3. High Availability and Fault Tolerance: Hazelcast automatically replicates data across multiple nodes to ensure high availability and fault tolerance. If a node fails, the data is automatically redistributed to other nodes in the cluster, ensuring uninterrupted access to the data.

4. Distributed Caching: Hazelcast can be used as a distributed cache, where frequently accessed data is stored in memory across the cluster, providing fast data retrieval and reducing the load on the underlying data sources.

5. Event Streaming: Hazelcast supports event-driven programming by providing an event journal that allows you to capture and process data change events in real-time. This enables building reactive applications and implementing event-driven architectures.

6. Integration with Various Technologies: Hazelcast integrates with popular frameworks and technologies, such as Java, .NET, Spring, Hibernate, Apache Kafka, Apache Spark, and more. This allows you to leverage Hazelcast within your existing application stack.

7. Clustering and Scaling: Hazelcast supports dynamic cluster formation, allowing nodes to join and leave the cluster without affecting the overall system. It also provides automatic load balancing and data rebalancing as the cluster size changes, ensuring efficient utilization of resources.

Overall, Hazelcast provides a powerful and flexible platform for distributed computing, in-memory caching, and event streaming. It is suitable for a wide range of use cases, including high-performance data processing, real-time analytics, caching, and improving application scalability and resilience.

### Hazelcast distributed cache
Hazelcast Distributed Cache refers to the caching capabilities provided by the Hazelcast in-memory data grid (IMDG). It allows you to store and access data in a distributed manner across a cluster of nodes.

In a distributed cache, data is stored in memory across multiple nodes instead of being stored in a single location. This enables faster data access and reduces the load on the underlying data sources or databases. By distributing the cache across a cluster, you can leverage the combined memory capacity of multiple nodes, providing greater storage capacity and better performance.

Hazelcast provides a simple and intuitive API for working with distributed caching. It offers a distributed map data structure called `IMap`, which behaves similarly to a standard Java `Map` but operates in a distributed manner. You can store key-value pairs in the IMap, and Hazelcast automatically distributes the data across the cluster.

Some key features and benefits of Hazelcast Distributed Cache include:

High Performance: By storing data in-memory across multiple nodes, Hazelcast Distributed Cache provides fast and low-latency data access, leading to improved application performance.

1. Scalability: The cache can scale horizontally by adding more nodes to the cluster. As the cluster grows, the cache can handle larger data sets and increased request loads.

2. Fault Tolerance: Hazelcast automatically replicates data across nodes, ensuring data availability even if a node fails. In case of node failure, the data is automatically redistributed to the remaining nodes.

3. Elasticity: Nodes can be dynamically added or removed from the cluster without interrupting the availability or functionality of the cache.

4. Consistency: Hazelcast offers configurable consistency models for cache operations, allowing you to choose between strong or eventual consistency based on your application requirements.

5. Integration: Hazelcast Distributed Cache can be easily integrated into various application frameworks and technologies, providing seamless caching capabilities for your applications.

By utilizing Hazelcast Distributed Cache, you can optimize your application's performance by caching frequently accessed data in memory, reducing the need for repetitive expensive database or remote service calls. It is particularly useful in scenarios where fast data access and low latency are critical, such as improving response times in web applications, speeding up data-intensive operations, or reducing the load on external systems.

### Event Streaming Hazelcast
Hazelcast provides event streaming capabilities through its built-in publish-subscribe (pub-sub) messaging system called the Distributed Event Journal. The Distributed Event Journal allows you to capture, publish, and consume events in a distributed and scalable manner within the Hazelcast cluster.

Here's how event streaming is achieved in Hazelcast:

1. Event Journal Configuration: You configure the Distributed Event Journal in Hazelcast by specifying the desired settings such as the name of the journal, capacity, time-to-live (TTL) for events, and other relevant parameters.

2. Publishing Events: To publish an event, you write it to the Distributed Event Journal using the provided API. The event can be any data structure or object that represents the information you want to publish. Hazelcast ensures that the event is persisted and distributed across the cluster.

3. Subscribing to Events: Consumers interested in consuming events can subscribe to the Distributed Event Journal. Multiple consumers can subscribe to the same journal, and they will receive events in parallel.

4. Event Consumption: Consumers receive events from the Distributed Event Journal using the subscription mechanism. Hazelcast provides APIs to fetch events from the journal based on various criteria such as sequence numbers, time ranges, or the availability of new events.

5. Event Processing: Once consumers receive events, they can process them according to their application logic. This may involve performing real-time analytics, triggering actions or workflows, updating application state, or forwarding events to other systems.

6. Event Replay: Hazelcast allows consumers to replay events from a specific point in time. This is useful for scenarios where you need to rebuild application state or analyze events retroactively.

The Distributed Event Journal in Hazelcast provides durability and fault tolerance by replicating events across multiple nodes in the cluster. If a node fails, the events are still accessible from other nodes, ensuring data availability.

It's important to note that while the Distributed Event Journal in Hazelcast provides event streaming capabilities within the Hazelcast cluster, if you need to integrate with external event streaming systems or frameworks like Apache Kafka or Apache Flink, you can leverage the connectors and integrations provided by Hazelcast to facilitate seamless data flow between systems.

Overall, Hazelcast's Distributed Event Journal enables event streaming within the Hazelcast cluster, allowing you to build reactive, event-driven applications and systems that can process and react to events in real-time.

### Example with Spring Boot
`build.gradle`
```groovy
plugins {
	id 'java'
	id 'org.springframework.boot' version '2.7.14-SNAPSHOT'
	id 'io.spring.dependency-management' version '1.0.15.RELEASE'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	sourceCompatibility = '1.8'
}

repositories {
	mavenCentral()
	maven { url 'https://repo.spring.io/milestone' }
	maven { url 'https://repo.spring.io/snapshot' }
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.boot:spring-boot-starter-cache'
	implementation 'com.hazelcast:hazelcast-all:4.0.2'


	runtimeOnly 'org.postgresql:postgresql'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

tasks.named('test') {
	useJUnitPlatform()
}
```
`hazelcast.xml`
```xml
<hazelcast
        xsi:schemaLocation="http://www.hazelcast.com/schema/config
        http://www.hazelcast.com/schema/config/hazelcast-config-3.12.12.xsd"
        xmlns="http://www.hazelcast.com/schema/config"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <instance-name>XML_Hazelcast_Instance</instance-name>
</hazelcast>
```
`HazelcastApplication.java`
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;

@EnableCaching
@SpringBootApplication
public class HazelcastApplication {

	public static void main(String[] args) {
		SpringApplication.run(HazelcastApplication.class, args);
	}

}
```
`CompanyApplicationController.java`
```java
package com.example.Hazelcast.controller;

import com.example.Hazelcast.model.Employee;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
@RequestMapping("/v1/")
class CompanyApplicationController {
    @Cacheable(value = "employee")
    @GetMapping("employee/{id}")
    public Employee getSubscriber(@PathVariable("id") int id) throws
            InterruptedException {
        System.out.println("Finding employee information with id " + id + " ...");
        Thread.sleep(5000);
        return new Employee(id, "John Smith", "CS");
    }
}
```
### Another Sample Spring Boot Example
`build.gradle`
```groovy
plugins {
	id 'java'
	id 'org.springframework.boot' version '2.7.14-SNAPSHOT'
	id 'io.spring.dependency-management' version '1.0.15.RELEASE'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	sourceCompatibility = '1.8'
}

repositories {
	mavenCentral()
	maven { url 'https://repo.spring.io/milestone' }
	maven { url 'https://repo.spring.io/snapshot' }
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.boot:spring-boot-starter-cache'
	implementation 'com.hazelcast:hazelcast-spring:4.2.1'
	implementation 'com.hazelcast:hazelcast:4.2.1'
	runtimeOnly 'org.postgresql:postgresql'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

tasks.named('test') {
	useJUnitPlatform()
}
```
`hazelcast.xml`
```xml
<hazelcast xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.hazelcast.com/schema/config
           http://www.hazelcast.com/schema/config/hazelcast-config-4.1.xsd">
    <instance-name>my-instance</instance-name>
    <network>
        <join>
            <multicast enabled="false"/>
            <tcp-ip enabled="true">
                <member>localhost</member>
            </tcp-ip>
        </join>
    </network>
</hazelcast>
```
`HazelcastApplication.java`
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;

@SpringBootApplication
public class HazelcastApplication {

	public static void main(String[] args) {
		SpringApplication.run(HazelcastApplication.class, args);
	}

}
```
`SimpleController.java`
```java
package com.example.Hazelcast.controller;

import com.hazelcast.core.HazelcastInstance;
import com.hazelcast.map.IMap;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class SimpleController {
    @Autowired
    private HazelcastInstance hazelcastInstance;

    @GetMapping("/hello/{name}")
    public String sayHello(@PathVariable String name) throws InterruptedException {
        IMap<String, String> cache = hazelcastInstance.getMap("myCache");
        if (cache.containsKey(name)) {
            return cache.get(name);
        } else {
            System.out.println("Hello waiting for 5sec..");
            Thread.sleep(5000);
            String message = "Hello, " + name + "!";
            cache.put(name, message);
            return message;
        }
    }
}
```






