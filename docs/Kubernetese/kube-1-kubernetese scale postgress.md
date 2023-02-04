---
layout: default
title: Getting Started Spring Reactor
parent: Kubernetes
grand_parent: Spring Boot
nav_order: 2
---
# Scale postgres DB in kubernetes
In `Kubernetes`, you can scale a `PostgreSQL` database by increasing or decreasing the number of replicas in a `StatefulSet`. This allows you to handle an increase in traffic and number of connections by creating additional replicas of your database.

To achieve this, you need to define a `Horizontal Pod Autoscaler` (HPA) that monitors the number of connections to the database and scales the number of replicas accordingly. The HPA will use metrics like `CPU utilization`, `memory usage`, and `database connection count` to determine when to scale.

For example, if you set the HPA to increase the number of replicas when the number of database connections exceeds a certain threshold, the HPA will create additional replicas of the PostgreSQL database to handle the increased traffic.

This way, you can ensure that your database is able to handle an increase in the number of connections and traffic, without any downtime or disruption to your application.

### Here is an example YAML file to deploy a PostgreSQL database in Kubernetes using a StatefulSet and HPA:
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgres
spec:
  selector:
    matchLabels:
      app: postgres
  serviceName: postgres-svc
  replicas: 1
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
        - name: postgres
          image: postgres:12.4
          ports:
            - containerPort: 5432
          env:
            - name: POSTGRES_USER
              value: "postgres"
            - name: POSTGRES_PASSWORD
              value: "postgres"
            - name: POSTGRES_DB
              value: "postgres"
          volumeMounts:
            - name: data
              mountPath: /var/lib/postgresql/data
  volumeClaimTemplates:
    - metadata:
      name: data
      annotations:
        volume.beta.kubernetes.io/storage-class: "standard"
      spec:
        accessModes: [ "ReadWriteOnce" ]
        resources:
          requests:
            storage: 2Gi
---
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: postgres-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: StatefulSet
    name: postgres
  minReplicas: 1
  maxReplicas: 5
  metrics:
    - type: Object
      object:
        target:
          apiVersion: extensions/v1beta1
          kind: Ingress
          name: postgres-ingress
        metricName: postgres-connections
        targetValue: 1000
```

