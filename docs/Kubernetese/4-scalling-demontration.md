---
layout: default
title: Auto Scaling Demo 
parent: Kubernetes
nav_order: 4
---
# Auto Scaling Demonstration with full-fledged application(api-caller)
In this example we have three Docker images: one for the front-end application and two for the back-end services named "service1" and "service2."

Our task is to create a comprehensive example of deploying these three services within a Kubernetes cluster while ensuring the following requirements are met:

1. The front-end application must be accessible from the outside.
2. The front-end application should consistently call the back-end service1.
3. Service1 is required to make HTTP requests to service2.
4. All applications must be designed for scalability based on CPU and Memory limits.

---
let's do this...
* Creating a namespace for the app deployment(`namespace.yml`):
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: my-app
```
* Front-end Deployment and Service(`front-end.yml`):
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
  namespace: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
        - name: frontend
          image: a1anjanjana/api-caller:latest
          ports:
            - containerPort: 3000
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"

---
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
  namespace: my-app
spec:
  selector:
    app: frontend
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 3000
  type: NodePort
# type: LoadBalancer
```
### ingress deployment
```yml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: frontend-ingress
  namespace: my-app
spec:
  rules:
    - host: your.domain.com  # Replace with your actual domain
      http:
        paths:
          - pathType: Prefix
            path: "/"
            backend:
              service:
                name: frontend-service
                port:
                  number: 3000

```
### Service-1 deployment 
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: service1-deployment
  namespace: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: service1
  template:
    metadata:
      labels:
        app: service1
    spec:
      containers:
        - name: service1
          image: a1anjanjana/service-1:latest
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"
          env:
            - name: SERVICE_2_API_URL
              value: "http://service2-service:8080"

---
apiVersion: v1
kind: Service
metadata:
  name: service1-service
  namespace: my-app
spec:
  selector:
    app: service1
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```
### service-2 deployment 
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: service2-deployment
  namespace: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: service2
  template:
    metadata:
      labels:
        app: service2
    spec:
      containers:
        - name: service2
          image: a1anjanjana/service-2:latest
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"

---
apiVersion: v1
kind: Service
metadata:
  name: service2-service
  namespace: my-app
spec:
  selector:
    app: service2
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```

## Troubleshooting
### Check ingress controller installed and running
````markdown
kubectl get pods -n ingress-nginx                                               

Output:
NAME                                        READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-j4nsv        0/1     Completed   0          176m
ingress-nginx-admission-patch-4n47t         0/1     Completed   0          176m
ingress-nginx-controller-7799c6795f-g2fpx   1/1     Running     0          176m
````
### Create minikube tunnel
```markdown
minikube tunnel
```

### Update hostsfile
```markdown
127.0.0.1       your.domain.com
```
* On macOS is minikube installed using docker desktop then use ip 127.0.0.1 otherwise use minikube cluster ip

```markdown
minikube ip
```
Now you should be able to access `your.domain.com` in browser. If you send multiple requests, you can visualize pods are auto-scaling. 

### api-caller front-end app
* Github link: (https://github.com/link2anjan/api-caller)

* The Host URL should be service1 api URL. 

* In the given deployment use the following URLs for testing
    * GET http://service1-service:8080/hello
    * GET http://service1-service:8080/hello-all (service-1 call REST API to Service-2)
    * PUT http://service1-service:8080/hey
    * POST http://service1-service:8080/hey
    * PATCH http://service1-service:8080/hey
    * DELETE http://service1-service:8080/hey

---
# Communicating services between different namespaces
In this example I'm will deploy service-2 in different namespace. It is possible to communicate between different namespaces. Here we have to use below format. 
```markdown
service2_url = "http://service2.namespace2.svc.cluster.local"
```
## Example:
### Creating new namespace
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: my-app-2
```
### Service-2 deployment 
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: service2-deployment
  namespace: my-app-2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: service2
  template:
    metadata:
      labels:
        app: service2
    spec:
      containers:
        - name: service2
          image: a1anjanjana/service-2:latest
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"

---
apiVersion: v1
kind: Service
metadata:
  name: service2-service
  namespace: my-app-2
spec:
  selector:
    app: service2
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```
### Service-1 deployment
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: service1-deployment
  namespace: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: service1
  template:
    metadata:
      labels:
        app: service1
    spec:
      containers:
        - name: service1
          image: a1anjanjana/service-1:latest
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"
          env:
            - name: SERVICE_2_API_URL
              value: "http://service2-service.my-app-2.svc.cluster.local:8080"

---
apiVersion: v1
kind: Service
metadata:
  name: service1-service
  namespace: my-app
spec:
  selector:
    app: service1
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```

![](../../assets/images/docs/screen-demo.png)

