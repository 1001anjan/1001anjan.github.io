---
layout: default
title: Hazelcast with Cloud
parent: Hazelcast
grand_parent: Spring Boot
nav_order: 4
---
### To use Hazelcast with Spring Boot in an AWS cloud environment
Create a `hazelcast.xml` file in the `src/main/resources` directory to configure Hazelcast:
```xml
<hazelcast xsi:schemaLocation="http://www.hazelcast.com/schema/config hazelcast-config-3.12.xsd"
           xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <network>
        <join>
            <tcp-ip enabled="false"/>
            <multicast enabled="false"/>
            <aws enabled="true">
                <access-key>YOUR_AWS_ACCESS_KEY</access-key>
                <secret-key>YOUR_AWS_SECRET_KEY</secret-key>
                <region>YOUR_AWS_REGION</region>
            </aws>
        </join>
    </network>

    <cache name="myCache">
        <max-size>10000</max-size>
        <eviction size="10000" max-size-policy="ENTRY_COUNT" eviction-policy="LFU"/>
        <time-to-live-seconds>600</time-to-live-seconds>
    </cache>

</hazelcast>
```
### To configure Hazelcast with GCP and Kubernetes, you can follow these steps:
1. Set up a Kubernetes cluster on GCP:
   * Log in to your GCP Console.
   * Navigate to the Kubernetes Engine service. 
   * Create a new cluster with the desired configuration, selecting the appropriate machine types, number of nodes, and networking options.
   * Wait for the cluster to be created.
2. Deploy Hazelcast in the Kubernetes cluster:
    * Create a Hazelcast deployment file, `hazelcast.yaml`, to define the Hazelcast deployment and service resources. Here's an example:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hazelcast
  labels:
    app: hazelcast
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hazelcast
  template:
    metadata:
      labels:
        app: hazelcast
    spec:
      containers:
        - name: hazelcast
          image: hazelcast/hazelcast:latest
          ports:
            - containerPort: 5701
          resources:
            limits:
              memory: 512Mi
            requests:
              memory: 256Mi
---
apiVersion: v1
kind: Service
metadata:
  name: hazelcast-service
  labels:
    app: hazelcast
spec:
  selector:
    app: hazelcast
  ports:
    - protocol: TCP
      port: 5701
      targetPort: 5701
```
This example deploys Hazelcast with three replicas and exposes port 5701 for communication.

3. This example deploys Hazelcast with three replicas and exposes port 5701 for communication.
* Apply the Hazelcast deployment and service YAML files using the `kubectl` command:
```markdown
kubectl apply -f hazelcast.yaml
```
4. Configure the Spring Boot application to connect to the Hazelcast cluster:
* Add the Hazelcast dependency to your `pom.xml` file:
```xml
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-kubernetes</artifactId>
</dependency>
```
* Create a `hazelcast.yaml` file in the `src/main/resources` directory to configure the Hazelcast Kubernetes discovery:
```yml
hazelcast:
  discovery:
    discovery-strategies:
      - class: com.hazelcast.kubernetes.HazelcastKubernetesDiscoveryStrategy
        properties:
          service-dns: hazelcast-service.default.svc.cluster.local
          service-dns-timeout: "5"
          service-name: hazelcast-service
          namespace: default
```
This configuration uses the `HazelcastKubernetesDiscoveryStrategy` to discover and connect to the `Hazelcast` cluster running in the Kubernetes environment. Adjust the `service-name` and `namespace` properties according to your Hazelcast service name and Kubernetes namespace.

5. Use Hazelcast caching in your Spring Boot application:

* Annotate the methods that you want to cache with the `@Cacheable` annotation from the `org.springframework.cache.annotation` package. For example:
```java
import org.springframework.cache.annotation.Cacheable;

// ...

@Cacheable("myCache")
public List<User> getAllUsers() {
    // Fetch users from your data source
}
```

6. Deploy your Spring Boot application to the Kubernetes cluster:
* Build your Spring Boot application into a container image and push it to a container registry.
* Deploy your application to the Kubernetes cluster, ensuring it has access to the Hazelcast cluster and the necessary configuration.