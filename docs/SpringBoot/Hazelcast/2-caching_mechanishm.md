---
layout: default
title: Caching
parent: Hazelcast
grand_parent: Spring Boot
nav_order: 2
---
### Caching
Hazelcast, an open-source in-memory data grid platform, provides various caching mechanisms to improve the performance and scalability of applications. Here are some of the different caching mechanisms available in Hazelcast:

1. Near Cache: Near Cache is a local cache that sits close to the application and stores frequently accessed data from the underlying distributed cache. It helps reduce the network round trips by serving data from the local cache, thereby improving the overall application performance.

2. Distributed Cache: Hazelcast allows you to distribute the cache across a cluster of nodes. It partitions the data and distributes it across the nodes, providing high availability and scalability. Each node holds a portion of the cache, enabling parallel processing and reducing the load on individual nodes.

3. Replicated Cache: Replicated Cache is a type of distributed cache where the entire cache data is replicated on each node in the cluster. This mechanism provides high availability as each node can serve the data independently without relying on other nodes. However, it may consume more memory as the data is duplicated across nodes.

4. Partitioned Cache: Partitioned Cache is another type of distributed cache where the cache data is partitioned across the cluster nodes based on a configurable key. Each node owns a specific set of cache entries, allowing for parallel processing and improved scalability. Partitioning also helps distribute the load across the cluster.

5. Write-Through and Write-Behind Caches: Hazelcast supports both write-through and write-behind caching strategies. With write-through caching, every write operation updates the cache and the underlying data store simultaneously. In contrast, with write-behind caching, write operations update the cache immediately and asynchronously update the underlying data store at a later time, improving the write performance.

6. Expiration and Eviction Policies: Hazelcast offers various expiration and eviction policies to manage the lifecycle of cache entries. You can set expiration times to automatically remove entries from the cache after a certain period. Eviction policies help manage the cache size by removing less frequently used entries based on strategies like least recently used (LRU), least frequently used (LFU), or random eviction.

These caching mechanisms in Hazelcast provide flexibility and performance optimization options for applications by reducing network latency, improving data access, and enabling efficient data distribution across clusters.

### Caching Topologies
To use Hazelcast as a distributed cache, you can choose one of the following topologies:

* Embedded mode: In this mode, the application and the cached data are stored on the same device. When a new entry is written to the cache, Hazelcast takes care of distributing it to the other members.

* Client/server mode: In this mode, the cached data is separated from the application. Hazelcast members run on dedicated servers and applications connect to them through clients.

### Embedded mode
* Advantages: Data access is faster because applications don’t need to send a request to the cache cluster over the network.
* Disadvantages: Hazelcast can be embedded only in Java applications. Each new instance of your application adds a new member to the cluster even if you don’t it.

### Client/server mode
* Advantages: Supports independent scaling of the application and the cache cluster. Allows you to write polyglot applications that can all connect to the same cache cluster.
* Disadvantages: To read from a cache or write to it, clients need to make network requests, which leads to higher latency than embedded mode.

### Embedded caching with Hazelcast in a Spring Boot application:
`pom.xml`
```xml
<dependencies>
    <!-- Other dependencies -->
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-cache</artifactId>
    </dependency>
</dependencies>
```
### Configure Hazelcast:
`HazelcastConfig.java`
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import com.hazelcast.config.Config;
import com.hazelcast.core.HazelcastInstance;
import com.hazelcast.spring.cache.HazelcastCacheManager;

@Configuration
public class HazelcastConfig {
    
    @Bean
    public Config hazelcastConfig() {
        return new Config();
    }
    
    @Bean
    public HazelcastInstance hazelcastInstance(Config hazelcastConfig) {
        return Hazelcast.newHazelcastInstance(hazelcastConfig);
    }
    
    @Bean
    public HazelcastCacheManager cacheManager(HazelcastInstance hazelcastInstance) {
        return new HazelcastCacheManager(hazelcastInstance);
    }
}
```
This configuration class creates a Hazelcast instance and a HazelcastCacheManager bean to manage the caches.
### Enable Caching:
`YourApplication.java`
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;

@SpringBootApplication
@EnableCaching
public class YourApplication {
    
    public static void main(String[] args) {
        SpringApplication.run(YourApplication.class, args);
    }
}
```
### Use Caching:
`YourService.java`
```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

@Service
public class YourService {
    
    @Cacheable("yourCacheName")
    public YourData getData(String id) {
        // Logic to retrieve data from a data source
        return yourData;
    }
}
```
### Hazelcast client-server topology in a Spring Boot application:
`pom.xml`
```xml
<dependencies>
    <!-- Other dependencies -->
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast</artifactId>
    </dependency>
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast-client</artifactId>
    </dependency>
</dependencies>
```
### Configure Server:
Set up a Hazelcast server instance by creating a configuration file named `hazelcast.xml` in the `src/main/resources` directory. Here's a sample configuration:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<hazelcast xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.hazelcast.com/schema/config
                               http://www.hazelcast.com/schema/config/hazelcast-config-4.3.xsd">
    <network>
        <port auto-increment="true">5701</port>
        <join>
            <multicast enabled="false"/>
            <tcp-ip enabled="true">
                <member>localhost</member>
            </tcp-ip>
        </join>
    </network>
</hazelcast>
```
`YourApplication.java`
```java
import com.hazelcast.client.config.ClientConfig;
import com.hazelcast.client.config.ClientNetworkConfig;
import com.hazelcast.client.config.ClientUserCodeDeploymentConfig;
import com.hazelcast.client.HazelcastClient;
import com.hazelcast.core.HazelcastInstance;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class YourApplication {

    public static void main(String[] args) {
        SpringApplication.run(YourApplication.class, args);
    }

    @Bean
    public HazelcastInstance hazelcastInstance() {
        ClientConfig config = new ClientConfig();
        ClientNetworkConfig networkConfig = config.getNetworkConfig();
        networkConfig.addAddress("localhost:5701"); // Configure the server address

        // Additional configuration if needed
        // config.setUserCodeDeploymentConfig(new ClientUserCodeDeploymentConfig().addClass(MyClass.class));
        // config.setInstanceName("my-instance");
        // ...

        return HazelcastClient.newHazelcastClient(config);
    }
}
```
In this example, we create a `HazelcastInstance` bean by configuring a `ClientConfig` object. The server address is specified in the addAddress method of the `ClientNetworkConfig`. You can also include additional configuration options as needed.

### Use Caching:
Once the Hazelcast client is configured, you can use it for caching in your service or repository classes. Follow the same steps as mentioned in the previous example for using caching with Hazelcast embedded mode.

### Near Cache in Hazelcast:
Near Cache in Hazelcast is a local cache that sits close to the client or application and stores frequently accessed data from the underlying distributed cache. It helps improve application performance by reducing the need for network round trips to fetch data from the remote cache.

### Advantages of Near Cache:
* Improved Performance: Near Cache reduces network latency by serving data from the local cache, eliminating the need to fetch data from the remote cache. This results in faster data access and improved overall application performance.
* Reduced Network Traffic: With Near Cache, data is retrieved and stored locally, reducing the amount of network traffic between the client and the remote cache. This can significantly decrease the load on the network and improve scalability.
* Lower Latency: Since data is stored locally, access to frequently used data is faster due to the reduced network round trips. This lowers the overall latency of accessing cached data.
* Consistency: Near Cache keeps the data in sync with the remote cache by automatically invalidating or updating the cached data when changes occur in the remote cache. This ensures data consistency across the distributed cache.

### Disadvantages of Near Cache:
* Increased Memory Usage: Near Cache requires additional memory to store the cached data locally. Depending on the size of the cache and the amount of data stored, this can lead to increased memory consumption.
* Staleness of Data: Near Cache introduces a level of eventual consistency. If data is updated in the remote cache, it may take some time for the changes to be propagated to the Near Cache. This can result in temporarily stale data until the Near Cache is refreshed.
* Maintenance Overhead: Near Cache introduces an additional layer of caching that needs to be managed and maintained. This includes handling cache eviction, cache updates, and cache synchronization between the client and the remote cache.

### Here's an example of how you can configure and use Near Cache in a Spring Boot application with Hazelcast:
`pom.xml`
```xml
<dependencies>
    <!-- Other dependencies -->
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast</artifactId>
    </dependency>
    <dependency>
        <groupId>com.hazelcast</groupId>
        <artifactId>hazelcast-client</artifactId>
    </dependency>
</dependencies>
```
### Configure Hazelcast Client:
Create a configuration class to configure Hazelcast client in your application. For example, create a `HazelcastClientConfig.java` file:
