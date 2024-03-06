---
layout: default
title: hazelcast.xml
parent: Hazelcast
nav_order: 7
---
### Here's an example of a complete hazelcast.xml file 
```xml
<hazelcast xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.hazelcast.com/schema/config
           http://www.hazelcast.com/schema/config/hazelcast-config-4.2.xsd">

    <!-- Cluster Name -->
    <cluster-name>my-cluster</cluster-name>

    <!-- Network Configuration -->
    <network>
        <!-- Join Configuration -->
        <join>
            <!-- Multicast Configuration (for discovery in the same network) -->
            <multicast enabled="true">
                <multicast-group>224.2.2.3</multicast-group>
                <multicast-port>54327</multicast-port>
            </multicast>
            <!-- TCP/IP Configuration (for static IP-based discovery) -->
            <tcp-ip enabled="false">
                <interface>127.0.0.1</interface>
                <member-list>
                    <member>127.0.0.1</member>
                </member-list>
            </tcp-ip>
        </join>
    </network>

    <!-- Map Configuration -->
    <map name="my-map">
        <!-- In-Memory Format -->
        <in-memory-format>OBJECT</in-memory-format>
        <!-- Eviction Policy -->
        <eviction-policy>LRU</eviction-policy>
        <!-- Max Size Policy -->
        <max-size policy="PER_NODE">1000</max-size>
        <!-- Time-To-Live (Expiration) -->
        <time-to-live-seconds>3600</time-to-live-seconds>
    </map>

    <!-- Near Cache Configuration -->
    <near-cache name="my-near-cache">
        <!-- In-Memory Format -->
        <in-memory-format>BINARY</in-memory-format>
        <!-- Eviction Policy -->
        <eviction eviction-policy="LRU" max-size-policy="PER_NODE" size="1000"/>
        <!-- Time-To-Live (Expiration) -->
        <time-to-live-seconds>600</time-to-live-seconds>
        <!-- Invalidate Policy -->
        <invalidate-on-change>true</invalidate-on-change>
    </near-cache>

</hazelcast>
```
1. `<cluster-name>`: Specifies the name of the Hazelcast cluster. All members with the same cluster name will form a cluster and discover each other.
2. `<network>`: Configures the network settings for the Hazelcast cluster.
3. `<join>`: Specifies the discovery mechanism for cluster members.
    * `<multicast>`: Enables multicast-based discovery. Members in the same network can discover each other using multicast communication.
        * `<multicast-group>`: Specifies the multicast group IP address.
        * `<multicast-port>`: Specifies the multicast port number.
    * `<tcp-ip>`: Enables static IP-based discovery. Members connect to specific IP addresses to discover other members.
        * `<interface>`: Specifies the network interface to bind to.
        * `<member-list>`: Lists the IP addresses of the members to be discovered.
4. `<map>`: Configures the settings for a specific distributed map in Hazelcast.
    * `<name>`: Specifies the name of the distributed map.
    * `<in-memory-format>`: Specifies the format for storing map entries in memory (OBJECT or BINARY).
    * `<eviction-policy>`: Specifies the eviction policy when the map reaches its maximum size (e.g., LRU, LFU, etc.).
    * `<max-size>`: Specifies the maximum size of the map (policy can be PER_NODE or PER_PARTITION).
    * `<time-to-live-seconds>`: Specifies the time-to-live (expiration) duration in seconds for map entries.
5. `<near-cache>`: Configures a near cache for a specific distributed map.
   * `<name>`: Specifies the name of the distributed map associated with the near cache.
   * `<in-memory-format>`: Specifies the format for storing near cache entries in memory (OBJECT or BINARY).
   * `<eviction>`: Configures the eviction settings for the near cache (eviction-policy, max-size-policy, and size).
   * `<time-to-live-seconds>`: Specifies the time-to-live (expiration) duration in seconds for near cache entries.
   * `<invalidate-on-change>`: Specifies whether the near cache should be invalidated on map entry changes.

These are some of the commonly used elements in the `hazelcast.xml` file. However, Hazelcast provides many more configuration options and elements to fine-tune the behavior and performance of your distributed cache. 

### Here's an example that demonstrates how to configure a Spring Boot application with a distributed cache using Hazelcast, where the near cache is updated based on changes in the distributed cache in the server cache cluster.
```xml
<!-- Spring Boot Starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>

<!-- Hazelcast Integration -->
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```
```java
@SpringBootApplication
public class HazelcastNearCacheExampleApplication {

    public static void main(String[] args) {
        SpringApplication.run(HazelcastNearCacheExampleApplication.class, args);
    }

}
```
`application.properties`
```yaml
# Hazelcast Configuration
hazelcast.config=hazelcast.xml
```
`hazelcast.xml`
```xml
<hazelcast xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.hazelcast.com/schema/config
           http://www.hazelcast.com/schema/config/hazelcast-config-4.2.xsd">

    <!-- Cluster Name -->
    <cluster-name>my-cluster</cluster-name>

    <!-- Network Configuration -->
    <network>
        <!-- Join Configuration -->
        <join>
            <!-- Multicast Configuration (for discovery in the same network) -->
            <multicast enabled="true">
                <multicast-group>224.2.2.3</multicast-group>
                <multicast-port>54327</multicast-port>
            </multicast>
        </join>
    </network>

    <!-- Map Configuration -->
    <map name="my-distributed-map">
        <!-- Near Cache Configuration -->
        <near-cache name="my-near-cache">
            <!-- Invalidate Policy -->
            <invalidate-on-change>true</invalidate-on-change>
        </near-cache>
    </map>

</hazelcast>
```
In this configuration:
* `my-cluster` is the name of the Hazelcast cluster.
* `Multicast` is enabled for discovering members in the same network.
* There is a distributed map named `my-distributed-map` with a near cache named `my-near-cache`.
* The near cache is configured with `invalidate-on-change` set to true, indicating that it should be updated based on changes in the distributed cache.

```java
@Service
public class DistributedCacheService {

    @Autowired
    private HazelcastInstance hazelcastInstance;

    public void putToCache(String key, String value) {
        IMap<String, String> distributedMap = hazelcastInstance.getMap("my-distributed-map");
        distributedMap.put(key, value);
    }

    public String getFromCache(String key) {
        IMap<String, String> distributedMap = hazelcastInstance.getMap("my-distributed-map");
        return distributedMap.get(key);
    }

    public void removeFromCache(String key) {
        IMap<String, String> distributedMap = hazelcastInstance.getMap("my-distributed-map");
        distributedMap.remove(key);
    }
}
```
```java
@RestController
public class CacheController {

    @Autowired
    private DistributedCacheService cacheService;

    @PostMapping("/cache")
    public ResponseEntity<String> putToCache(@RequestParam String key, @RequestParam String value) {
        cacheService.putToCache(key, value);
        return ResponseEntity.ok("Value added to cache");
    }

    @GetMapping("/cache/{key}")
    public ResponseEntity<String> getFromCache(@PathVariable String key) {
        String value = cacheService.getFromCache(key);
        if (value != null) {
            return ResponseEntity.ok(value);
        }
        return ResponseEntity.notFound().build();
    }

    @DeleteMapping("/cache/{key}")
    public ResponseEntity<String> removeFromCache(@PathVariable String key) {
        cacheService.removeFromCache(key);
        return ResponseEntity.ok("Value removed from cache");
    }
}
```
In this example, the `DistributedCacheService` class interacts with the distributed cache using the Hazelcast instance. The `CacheController` provides REST endpoints to put a value into the cache, retrieve a value from the cache, and remove a value from the cache.

When a value is put into or removed from the distributed cache, the near cache associated with the `my-near-cache` configuration will be updated automatically due to the `invalidate-on-change` setting.
