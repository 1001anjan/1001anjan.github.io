---
layout: default
title: Headless Service
parent: Kubernetes
nav_order: 6
---
# Headless Service
In Kubernetes, a headless service is a type of service that is used to expose a set of pods without assigning them a stable IP address or load balancing traffic to them. Unlike a regular service (ClusterIP, NodePort, or LoadBalancer), which provides a single entry point and load balancing for a set of pods, a headless service does not have a ClusterIP and does not load balance traffic. Instead, it allows direct DNS-based discovery of individual pod IPs.

Here's a use case and example of when you might use a headless service in Kubernetes:

## Use Case: Stateful Applications
One common use case for headless services is in stateful applications, such as databases, where each pod has a unique identity and maintaining stable DNS entries for each pod is important for scaling, failover, and data consistency.

### Example: StatefulSet with a Headless Service
Let's say you have a StatefulSet that manages a group of stateful pods, such as a database cluster. Each pod in the StatefulSet has a unique identity, and you want to be able to address them individually for tasks like backup, scaling, or data replication.

* Create a Headless Service:
```yml
apiVersion: v1
kind: Service
metadata:
  name: my-database
  labels:
    app: database
spec:
  clusterIP: None   # This specifies that it's a headless service.
  selector:
    app: database
  ports:
    - protocol: TCP
      port: 3306     # Port for MySQL, adjust as needed.
```

In this example, we've created a headless service called `my-database` for a database application. Setting `clusterIP` to `None` makes it headless.

* Create a StatefulSet that Uses the Headless Service:
```yml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: my-database  # Specify the headless service name.
  replicas: 3
  selector:
    matchLabels:
      app: database
  template:
    metadata:
      labels:
        app: database
    spec:
      containers:
        - name: mysql
          image: mysql
          ports:
            - containerPort: 3306
          # ... other pod configuration ... 
```
The `serviceName` field in the StatefulSet spec is set to the name of the headless service (`my-database`), allowing the pods to be named and addressed individually.

Now, you can address each pod individually using DNS. For example, you can access the first pod in the StatefulSet using the DNS name `mysql-0.my-database` and the second pod as `mysql-1.my-database`, and so on. This is particularly useful for stateful applications that rely on stable DNS names and unique identities for each pod.

In summary, headless services in Kubernetes are valuable for stateful applications that require individual pod identification and DNS-based discovery. They allow you to work with each pod as a separate entity while benefiting from Kubernetes orchestration features.






