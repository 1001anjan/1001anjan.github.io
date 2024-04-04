---
layout: default
title: Scale microservice depending on cup utilization
parent: Kubernetes
nav_order: 11
---
# kubernetes scale microservice depending on cup utilization  
To scale a microservice based on CPU utilization in Kubernetes, you can use the Horizontal Pod Autoscaler (HPA) feature. The HPA will automatically adjust the number of replicas in a deployment based on observed CPU utilization.

Here is a general process to set up HPA:

1. Create a deployment that manages your microservice
2. Annotate the deployment with the target CPU utilization
3. Create a HorizontalPodAutoscaler object that references the deployment
4. Verify that the HPA is properly scaling the replicas of your deployment

Here is an example YAML configuration for an HPA:
```yaml
apiVersion: autoscaling/v2beta1
kind: HorizontalPodAutoscaler
metadata:
  name: my-microservice-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-microservice-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      targetAverageUtilization: 50
```

In this example, the HPA will target a CPU utilization of 50% and scale the replicas of the deployment named "my-microservice-deployment" from a minimum of 1 replica to a maximum of 10 replicas.

Here is a complete example of deploying a Docker image and auto-scaling based on CPU utilization using Kubernetes and YAML configurations:

1. Deployment YAML:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-microservice-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-microservice
  template:
    metadata:
      labels:
        app: my-microservice
    spec:
      containers:
      - name: my-microservice
        image: my-microservice:latest
        resources:
          requests:
            cpu: 100m
        ports:
        - containerPort: 80
```
2. Horizontal Pod Autoscaler YAML:
```yaml
apiVersion: autoscaling/v2beta1
kind: HorizontalPodAutoscaler
metadata:
  name: my-microservice-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-microservice-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      targetAverageUtilization: 50
```
3. Apply the configurations using the `kubectl` command line tool:
```yaml
kubectl apply -f deployment.yaml
kubectl apply -f hpa.yaml
```
This will deploy your Docker image as a microservice and configure the HPA to monitor the CPU utilization of the deployment and adjust the number of replicas based on the target utilization.







