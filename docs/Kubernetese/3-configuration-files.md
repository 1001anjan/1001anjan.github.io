---
layout: default
title: Configuration Files
parent: Kubernetes
nav_order: 3
---
# Kubernetes Configurations
Kubernetes' configuration files are YAML or JSON files that define how Kubernetes resources should be created, updated, or deleted within a cluster. These files encapsulate the desired state of resources and allow you to manage your applications and infrastructure using declarative syntax. Kubernetes configuration files specify the properties and attributes of resources, such as pods, services, deployments, configmaps, and more.

Here are some commonly used Kubernetes configuration files:

1. Pod Configuration:
   A pod configuration file defines the characteristics of a single pod. It includes information about containers, volumes, environment variables, and more.
2. Service Configuration:
   A service configuration file defines a Kubernetes service, which provides networking and load balancing for pods. It includes the service type (ClusterIP, NodePort, LoadBalancer), selector to identify the target pods, and ports.
3. Deployment Configuration:
   A deployment configuration file defines how an application should be deployed and managed over time. It specifies the desired number of replicas, container specifications, update strategy, and more.
4. ConfigMap and Secret Configuration:
   ConfigMap and Secret configuration files define configuration data and sensitive information, respectively, that can be used by pods and containers.
5. Namespace Configuration:
   A namespace configuration file defines a namespace, allowing you to create isolated environments within the cluster.
6. Persistent Volume (PV) and Persistent Volume Claim (PVC) Configuration:
   PV and PVC configuration files define storage resources and claims, enabling stateful applications to store data persistently.
7. Horizontal Pod Autoscaler (HPA) Configuration:
   An HPA configuration file defines how to automatically scale the number of pods based on resource utilization.
8. Network Policy Configuration:
   A network policy configuration file defines network access rules for pods, allowing you to control communication between them.
9. Ingress Configuration:
   An ingress configuration file defines rules for routing external traffic to services within the cluster.
10. Custom Resource Definition (CRD) Configuration:
    A CRD configuration file defines custom resources, extending Kubernetes' capabilities with your own resource types.
11. Job and CronJob Configuration:
    Job and CronJob configuration files define batch processing tasks, which can be run once (Job) or scheduled periodically (CronJob).

Kubernetes configuration files are typically written in YAML format, but JSON is also supported. The structure of these files is defined by Kubernetes API objects and their associated fields. You can apply configuration files using the `kubectl apply -f <filename>` command, and Kubernetes will ensure that the desired state is achieved within the cluster.

These configuration files are essential for managing applications and infrastructure as code in a Kubernetes environment, allowing for version control, reproducibility, and consistent deployment practices.

# Examples:
## Pod configuration:
Here's an example of a simple pod configuration in YAML format:
```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-app
spec:
  containers:
    - name: my-container
      image: nginx:latest
    # Add more containers if needed
```
In this example:
* `apiVersion`: Specifies the version of the Kubernetes API being used. In this case, it's the core `v1` API.
* `kind`: Specifies the kind of Kubernetes resource. In this case, it's a `Pod`.
* `metadata`: Contains metadata about the pod, such as its `name` and `labels`.
* `spec`: Defines the desired state of the pod.
    * `containers`: Lists the containers within the pod.
        * `name`: The name of the container.
        * `image`: The Docker image to use for the container.

This configuration defines a pod named `my-pod` with a single container named `my-container`. The container uses the `nginx:latest` image, which is an `Nginx` web server. You can add more containers to the containers list if you need multiple containers in the same pod.

To create this pod using the `kubectl` command-line tool, save the configuration to a file (e.g., `pod.yaml`) and then run:
```markdown
kubectl apply -f pod.yaml
```

This will create the pod in your Kubernetes cluster according to the specified configuration.

## Deployment configuration
Here's an example of a simple deployment configuration in YAML format:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: nginx:latest
```
In this example:
* `apiVersion`: Specifies the version of the Kubernetes API for deployments. Here, it's `apps/v1`.
* `kind`: Specifies that this configuration defines a `Deployment`.
* `metadata`: Contains metadata about the deployment, such as its `name`.
* `spec`: Defines the desired state of the deployment.
    * `replicas`: Specifies the desired number of replicas (instances) for the deployment. In this case, it's set to `3`.
    * `selector`: Specifies how the replicas are selected.
        * `matchLabels`: Specifies the labels that the replicas must match. This is used to ensure that the replicas are associated with the right pods.
    * `template`: Defines the pod template that the deployment creates.
        * `metadata`: Contains metadata for the pod template.
            * `labels`: Labels applied to the pods created by the deployment.
        * `spec`: Defines the pod specification.
            * `containers`: Lists the containers within the pod, similar to the previous example.

This configuration defines a deployment named `my-deployment` with three replicas. The deployment ensures that there are always three instances of the pod, each containing a container based on the `nginx:latest` image.

To create this deployment, save the configuration to a file (e.g., `deployment.yaml`) and then run:

```markdown
kubectl apply -f deployment.yaml
```

## Service configuration
Here's an example of a simple service configuration in YAML format:
```yml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```
In this example:
* `apiVersion`: Specifies the version of the Kubernetes API for services. Here, it's `v1`.
* `kind`: Specifies that this configuration defines a `Service`.
* `metadata`: Contains metadata about the service, such as its `name`.
* `spec`: Defines the desired state of the service.
   * `selector`: Specifies the pods that the service should target. Pods with matching labels will be part of the service.
   * `ports`: Specifies the ports to expose on the service.
        * `protocol`: The protocol for the port (TCP in this case).
        * `port`: The port on the service.
        * `targetPort`: The port on the pods that the service should forward traffic to.
   * `type`: Specifies the service type. Here, it's `ClusterIP`, which exposes the service only within the cluster.

This configuration defines a service named `my-service` that targets pods with the label `app: my-app`. The service exposes port `80`, and incoming traffic to this port is forwarded to the pods' port `80`.

To create this service, save the configuration to a file (e.g., `service.yaml`) and then run:
```markdown
kubectl apply -f service.yaml
```
Kubernetes will create the service, and you'll be able to access the pods that match the labels via the service's IP and port within the cluster.

### Advantages of service configuration
Service configurations are essential in Kubernetes because they provide a way to enable network communication and load balancing to pods within the cluster. Services abstract away the complexity of directly dealing with individual pod IP addresses and provide a consistent way to access applications and services regardless of their dynamic nature or scaling changes.

Here are the main reasons why service configurations are needed in Kubernetes:

* Pod Abstraction: Pods in Kubernetes have dynamic IP addresses that can change due to scaling, rescheduling, or node failures. Services provide a stable and abstract way to communicate with pods regardless of their IP changes.
* Load Balancing: Services distribute incoming traffic across multiple pods that match the service's selector. This load balancing ensures even distribution of traffic and improved availability of applications.
* Service Discovery: Services provide a way to discover pods within the cluster. Clients (both inside and outside the cluster) can connect to a service by its DNS name, which resolves to the service's IP address.
* Exposing Ports: Services allow you to expose specific ports on pods and make them accessible to other pods or external clients. This is particularly useful for applications that run on non-standard ports.
* Cluster Internal Communication: Services enable communication between different parts of an application within the same cluster, even if the pods are running on different nodes.
* External Connectivity: Some service types (e.g., NodePort and LoadBalancer) allow you to expose services to external networks, making your applications accessible from outside the cluster.
* Centralized Configuration: Services provide a centralized configuration point for network-related settings. This separation of concerns allows developers to focus on application logic without worrying about networking complexities.
* Service Types: Different service types (ClusterIP, NodePort, LoadBalancer, ExternalName) cater to various use cases, from internal cluster communication to exposing applications externally.
* Health Checks: Services can perform health checks on pods and route traffic only to healthy instances, improving the overall reliability of applications.

Overall, service configurations play a crucial role in managing networking and communication in Kubernetes. They help abstract away the complexities of IP management, load balancing, and connectivity, allowing developers and operators to build and manage applications more effectively in dynamic and distributed environments.

### ClusterIP, NodePort, LoadBalancer, and ExternalName
Let's dive into each of the four service types in Kubernetes: ClusterIP, NodePort, LoadBalancer, and ExternalName. I'll explain what each type does and provide comparisons between them based on use cases.

1. ClusterIP: 
   * Description: ClusterIP is the default service type. It exposes the service on an internal IP within the cluster. This type makes the service accessible only from within the cluster.
   * Use Cases:
        * Internal communication between different parts of an application within the same cluster.
        * Services that should not be directly accessed from outside the cluster.
   * Comparison:
        * Only accessible from within the cluster.
        * Good for internal microservice communication.

    ```yml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-clusterip-service
    spec:
      selector:
        app: my-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
    ```
    In this example, the `my-clusterip-service` exposes pods labeled with `app: my-app` internally within the cluster. The service listens on port `80` and forwards traffic to the pods' port `8080`.
2. NodePort:
    * Description: NodePort exposes the service on a static port on each node in the cluster. Traffic sent to a node's IP on the specified NodePort is forwarded to the service.
    * Use Cases:
        * Accessing the service from outside the cluster during development or testing.
        * Load balancing traffic to multiple pods across nodes.
    * Comparison:
        * Accessible from outside the cluster.
        * Can be used for development or testing scenarios.

    ```yml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-nodeport-service
    spec:
      selector:
        app: my-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
      type: NodePort
    ```
3. LoadBalancer:
    * Description: LoadBalancer provisions an external load balancer (e.g., cloud provider's load balancer) to distribute traffic to the service. It also creates a NodePort and ClusterIP service.
    * Use Cases:
        * Exposing services to the internet or external networks.
        * Distributing incoming traffic across multiple pods.
    * Comparison:
        * Exposes services externally, often through a cloud provider's load balancer.
        * Suitable for production workloads requiring external access.

    ```yml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-loadbalancer-service
    spec:
      selector:
        app: my-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
      type: LoadBalancer
    
    ```
   This example creates an external load balancer provided by your cloud provider. The service becomes accessible externally with its own IP address and port 80. This type is often used to expose applications to the internet.
4. ExternalName:
    * Description: ExternalName does not expose pods. Instead, it maps the service to a DNS name. It's used to provide a custom alias for an external service.
    * Use Cases:
        * Referencing external services using a Kubernetes-style DNS name.
        * Migrating applications to Kubernetes that rely on external services.
    * Comparison:
        * Provides DNS-level abstraction to external services.
        * Useful for applications needing to integrate with external resources.

    ```yml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-external-service
    spec:
      type: ExternalName
      externalName: example.com
    ```
   In this example, the `my-external-service` is not used to expose pods. Instead, it acts as an alias to the external resource `example.com`. This is useful for integrating with external systems using a Kubernetes-style DNS name.

## How to create loadBalancer in minikube
it's possible to use the LoadBalancer service type in Minikube, but it requires a bit of extra setup. In Minikube, the LoadBalancer type usually won't provision an external load balancer provided by a cloud provider since Minikube is typically used for local development and testing. However, you can simulate the LoadBalancer behavior using Minikube's built-in addons.

Here's how you can set up and use the LoadBalancer service type in Minikube:

1. Enable the `metallb` Addon:
   Minikube provides an addon called `metallb` that simulates LoadBalancer behavior for services. To enable it, run:
   ```markdown
   minikube addons enable metallb
   ```
   
2. Configure `metallb`:
   After enabling the `metallb` addon, you need to configure its IP range. Create a `metallb-config.yaml` file with the following content:

    ```yml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      namespace: metallb-system
      name: config
    data:
      config: |
        address-pools:
        - name: default
          protocol: layer2
          addresses:
          - <IP_RANGE>
    ```
   Replace `<IP_RANGE>` with a range of IP addresses that is compatible with your local network setup.
    
    ### Example: 
    ```yml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      namespace: metallb-system
      name: config
    data:
      config: |
        address-pools:
        - name: default
          protocol: layer2
          addresses:
          - 192.168.100.1-192.168.100.254
    
    ```
    To replace <IP_RANGE> with a range of IP addresses that is compatible with your local network setup, you need to choose an IP address range that is not already in use by your network and is within the address space of your local network. This IP range will be used by the metallb addon to simulate the LoadBalancer behavior.

    Here's how you can determine a suitable IP range:

    * Check Your Local Network Setup:
        You'll need to identify an IP address range that is not being used by your local network. This should be within the private IP address ranges reserved for local networks, such as:

         * 10.0.0.0 - 10.255.255.255 (10.0.0.0/8)
         * 172.16.0.0 - 172.31.255.255 (172.16.0.0/12)
         * 192.168.0.0 - 192.168.255.255 (192.168.0.0/16)
    * Choose an IP Range:
       Within the selected private IP range, choose a subnet (CIDR notation) that is not already in use. For example, you might choose 192.168.100.0/24 if it's not being used by your network. This provides a range of IP addresses from 192.168.100.1 to 192.168.100.254.
3. Apply the Configuration:
   Apply the configuration using the `kubectl apply` command:
   ```markdown
   kubectl apply -f metallb-config.yaml
   ```
4. Create a LoadBalancer Service:
   Now you can create a LoadBalancer service as you would normally:

    ````yml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-loadbalancer-service
    spec:
      selector:
        app: my-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
      type: LoadBalancer
    ````
   
5. Access the LoadBalancer:
   The LoadBalancer IP address specified in your service configuration should now be accessible. You can get the external IP using:
    ```
   kubectl get svc my-loadbalancer-service
   ```
   
## ConfigMap and Secret Configuration:
### ConfigMap Configuration:
Let's say you want to store configuration data like environment variables for your application. You can use a ConfigMap to manage this data:
```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  DATABASE_URL: "mongodb://localhost:27017/mydb"
  API_KEY: "my-api-key"
```
In this example:
* `apiVersion`: Specifies the version of the Kubernetes API for ConfigMap.
* `kind`: Specifies that this configuration defines a ConfigMap.
* `metadata`: Contains metadata about the ConfigMap, such as its name.
* `data`: Defines key-value pairs for configuration data.

To create this ConfigMap, save the configuration to a file (e.g., `configmap.yaml`) and then run:
```markdown
kubectl apply -f configmap.yaml
```
### Secret Configuration:
Secrets are used to store sensitive data, such as passwords and tokens, in a more secure manner:
```yml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: YWRtaW4=   # base64-encoded "admin"
  password: cGFzc3dvcmQ=  # base64-encoded "password"
```
In this example:
* `apiVersion`: Specifies the version of the Kubernetes API for Secret.
* `kind`: Specifies that this configuration defines a Secret.
* `metadata`: Contains metadata about the Secret, such as its name.
* `type`: Specifies the type of secret. `Opaque` is the default type.
* `data`: Defines base64-encoded key-value pairs for sensitive data.

To create this Secret, save the configuration to a file (e.g., `secret.yaml`) and then run:
```markdown
kubectl apply -f secret.yaml
```

Keep in mind that while base64 encoding provides some level of obfuscation, it is not the most secure way to store sensitive data. Kubernetes Secrets are still more secure than plain text, but for high-security requirements, you might want to look into more advanced solutions.

### Deployment example
Here's an example of how you can reference a ConfigMap and a Secret in a Deployment configuration YAML file.

Let's assume you have a Deployment configuration for a simple application that requires configuration data and sensitive credentials:

Assuming you have a ConfigMap named `my-config` with `keys DATABASE_URL` and `API_KEY`, you can reference it in your Deployment configuration like this:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: my-app-image:latest
          envFrom:
            - configMapRef:
                name: my-config
```

In this example, the `envFrom` field under containers references the `my-config` ConfigMap. The keys and values from the ConfigMap will be injected as environment variables into the container.

### Secret Example:
Assuming you have a Secret named `my-secret` with keys `username` and `password`, you can reference it in your Deployment configuration like this:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: my-app-image:latest
          env:
            - name: USERNAME
              valueFrom:
                secretKeyRef:
                  name: my-secret
                  key: username
            - name: PASSWORD
              valueFrom:
                secretKeyRef:
                  name: my-secret
                  key: password
```
In this example, the `env` field under `containers` references the `my-secret` Secret using `secretKeyRef`. The specified keys' values will be injected as environment variables into the container.

## Namespace configuration
Here's an example of a Namespace configuration in Kubernetes:
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```
In this example, a Namespace named "my-namespace" is being created. Namespaces are used to provide a scope for resources within a Kubernetes cluster. They help in organizing and isolating resources, allowing multiple teams or projects to use the same cluster without interfering with each other's resources.

You would save this configuration in a .yaml file, such as `namespace.yaml`, and then apply it using the `kubectl` command:
```markdown
kubectl apply -f namespace.yaml
```
After applying the configuration, the "my-namespace" Namespace will be created in your Kubernetes cluster. You can then use this Namespace to deploy your resources like pods, services, deployments, etc., and they will be isolated within the specified Namespace.

Namespaces in Kubernetes are used to create virtual clusters within a physical cluster, helping in resource isolation, organization, and access control. Once you've created a Namespace, you can use it to deploy and manage your resources. Here's how you can use a Namespace:

* Deploy Resources: When deploying resources, specify the Namespace in the resource's metadata. Here's an example of a Deployment configuration specifying the Namespace:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  namespace: my-namespace
spec:
  replicas: 3
  template:
    spec:
      containers:
        - name: my-container
          image: nginx 
```
Deploy this configuration using `kubectl apply -f deployment.yaml`. The "my-app" Deployment will be created in the "my-namespace" Namespace.

* Access Resources: When interacting with resources in a specific Namespace, you need to explicitly mention the Namespace using the `-n` flag in `kubectl` commands. For example:
```markdown
kubectl get pods -n my-namespace
kubectl describe service/my-service -n my-namespace
```
* Switching Context: If you frequently work within a specific Namespace, you can set it as the default context so you don't have to specify the `-n` flag each time. Use the following command to set the default Namespace for your context:
```markdown
kubectl config set-context --current --namespace=my-namespace
```
* Deleting Resources: Deleting a Namespace will also delete all the resources within it. To delete a Namespace and its resources:
```markdown
kubectl delete namespace my-namespace
```
Remember that Namespaces provide logical isolation, but they do not provide strict security boundaries. They are more for organization and resource management. If you need stronger isolation, you should look into using other Kubernetes features like Network Policies or Role-Based Access Control (RBAC).

## Persistent Volume (PV) and Persistent Volume Claim (PVC) Configuration:
* Persistent Volume (PV) Configuration (pv.yaml):
```yml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: manual
  hostPath:
    path: /data/my-pv 
```
In this example, a PV named "my-pv" is created. It's using a `hostPath` type, meaning the storage is on the host machine's filesystem. You can replace this with other types like NFS, AWS EBS, etc. Adjust the `hostPath` to match your actual filesystem path. The PV has a capacity of 1GB, supports ReadWriteOnce access mode, and retains data even after the claim is deleted.

Apply the PV configuration with:
```markdown
kubectl apply -f pv.yaml
```
* Persistent Volume Claim (PVC) Configuration (pvc.yaml):
```yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
  storageClassName: manual
```
In this example, a PVC named "my-pvc" is created. It requests 500MB of storage and uses the `manual` storage class, which matches the storage class defined in the PV configuration.

Apply the PVC configuration with:
```markdown
kubectl apply -f pvc.yaml
```
* Binding PVC to PV:
  After the PVC is created, Kubernetes will automatically bind it to a suitable available PV that matches the requirements. You can see the binding with:
```markdown
kubectl get pvc my-pvc
```
* Using PVC in a Pod:
  To use the PVC in a Pod, you'd reference the PVC's name as the volume source in your Pod's configuration. Here's a snippet of a Pod configuration that uses the PVC:
```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx
      volumeMounts:
        - name: my-pvc-volume
          mountPath: /app/data
  volumes:
    - name: my-pvc-volume
      persistentVolumeClaim:
        claimName: my-pvc
```
This configuration mounts the PVC named "my-pvc" into the container at the path "/app/data".

Apply the Pod configuration with:
```markdown
kubectl apply -f pod.yaml
```
This way, the Pod can use the storage provided by the Persistent Volume through the Persistent Volume Claim.

## Horizontal Pod Autoscaler (HPA) Configuration:
Here's a complete example of how to configure a Horizontal Pod Autoscaler (HPA) in Kubernetes, along with descriptions for each section:

* Deployment Configuration (deployment.yaml):
  Let's start by creating a Deployment that we want to scale using the Horizontal Pod Autoscaler.
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app-container
          image: nginx
          resources:
            requests:
              cpu: 100m
```
In this example, we're creating a simple Deployment with one replica, running an Nginx container. The CPU request is set to 100 milliCPU.
* Horizontal Pod Autoscaler Configuration (hpa.yaml):
  Now, let's create an HPA that automatically scales the Deployment based on CPU utilization.
```yml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app-deployment
  minReplicas: 1
  maxReplicas: 5
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50 
```
Here's the breakdown of the HPA configuration:
* `scaleTargetRef`: Specifies the target resource for scaling, which is the Deployment named "my-app-deployment".
* `minReplicas`: Minimum number of replicas the Deployment should have.
* `maxReplicas`: Maximum number of replicas the Deployment can scale up to.
* `metrics`: Specifies the metrics used for scaling. In this case, we're using CPU utilization as the metric.
    * `type`: Type of metric, which is "Resource".
    * `resource`: Specifies the resource metric being used, which is "cpu".
        * `name`: The name of the resource being measured, which is "cpu".
        * `target`: Specifies the target utilization for scaling.
            * `type`: Type of target, which is "Utilization".
            * `averageUtilization`: The target average CPU utilization percentage, in this case, 50%.

### Applying Configurations:
Apply both the Deployment and HPA configurations using the following commands:
```markdown
kubectl apply -f deployment.yaml
kubectl apply -f hpa.yaml
```

### Observing Scaling:
As the load on the application increases, the HPA will automatically scale the Deployment up or down to maintain the target CPU utilization.

You can observe the HPA's behavior using the following command:
```markdown
kubectl describe hpa my-app-hpa
```

## Network Policy Configuration:
Here's a complete example of how to configure a Network Policy in Kubernetes:
* Create Namespace (namespace.yaml):
  If you haven't already, create a Namespace where you'll deploy your resources.
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace 
```
Apply the Namespace using:
```markdown
kubectl apply -f namespace.yaml
```
* Create Network Policy (network-policy.yaml):
  Let's create a Network Policy that allows traffic only from a specific set of pods and denies all other incoming traffic.
```yml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: my-network-policy
  namespace: my-namespace
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
    - Ingress
  ingress:
    - from:
        - podSelector:
            matchLabels:
              role: allowed-app 
```
Here's a breakdown of the Network Policy configuration:
* `podSelector`: Specifies the pods to which this policy applies, in this case, pods with the label `app: my-app`.
* `policyTypes`: Specifies the types of policies, which is `Ingress` in this case.
* `ingress`: Defines the ingress rules (incoming traffic rules).
    * `from`: Lists the sources allowed to access the selected pods.
        * `podSelector`: Specifies the label selector for the allowed pods, in this case, pods with the label `role: allowed-app`.

### Deploy Resources (deployment.yaml):
Let's create a sample Deployment to demonstrate the Network Policy.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
  namespace: my-namespace
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app-container
          image: nginx
```
Apply the Deployment using:
```markdown
kubectl apply -f deployment.yaml
```
### Label Pods (label-pods.yaml):
Let's label some pods that we want to allow access from in the Network Policy.
```yml
apiVersion: v1
kind: Pod
metadata:
  name: allowed-pod-1
  namespace: my-namespace
  labels:
    app: my-app
    role: allowed-app
spec:
  containers:
    - name: allowed-container
      image: busybox
      command: ["sleep", "3600"]
```
Apply the labeled Pod using:
```markdown
kubectl apply -f label-pods.yaml
```
### Apply Network Policy:
Apply the Network Policy using:
```markdown
kubectl apply -f network-policy.yaml
```
Now, only pods labeled with `role: allowed-app` can access pods labeled with `app: my-app` within the `my-namespace` Namespace. Other incoming traffic will be denied.

Remember, Network Policies require a network plugin that supports network policy enforcement, such as Calico or Cilium. The specific behavior and configuration might vary depending on your network plugin and Kubernetes setup.

## Ingress Configuration:
Here's a complete example of how to configure an Ingress resource in Kubernetes to expose a service:

* Create Namespace (namespace.yaml):
  If you haven't already, create a Namespace where you'll deploy your resources.
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace 
```
Apply the Namespace using:
```markdown
kubectl apply -f namespace.yaml
```

* Create Deployment and Service (deployment-service.yaml):
  Let's create a sample Deployment and a Service that we want to expose using Ingress.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
  namespace: my-namespace
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app-container
          image: nginx

---

apiVersion: v1
kind: Service
metadata:
  name: my-app-service
  namespace: my-namespace
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```
Apply the Deployment and Service using:
```markdown
kubectl apply -f deployment-service.yaml
```

* Create Ingress Resource (ingress.yaml):
  Now, let's create an Ingress resource to expose the Service.
```yml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  namespace: my-namespace
spec:
  rules:
    - host: myapp.example.com  # Change this to your domain
      http:
        paths:
          - pathType: Prefix
            path: "/"
            backend:
              service:
                name: my-app-service
                port:
                  number: 80
```
In this example, make sure to change `myapp.example.com` to the actual domain you intend to use. The Ingress routes incoming traffic from the specified host to the `my-app-service` Service.

Apply the Ingress using:
```markdown
kubectl apply -f ingress.yaml
```
* Update Hosts File:
  For testing purposes, you might need to update your local machine's hosts file to point the chosen domain to the IP address of your cluster. This is typically needed when you're testing on a local or non-production environment.

* Access the Application:
  Now, you should be able to access your application using the configured domain (e.g., `myapp.example.com` if you used that in the Ingress configuration).

Please note that the effectiveness of this example depends on your cluster setup and whether you have a functioning DNS system. Additionally, you might need to set up an Ingress Controller in your cluster for the Ingress resource to work. The process can vary based on the environment and tools you're using.

* Note:
    * You'll need to ensure that you have an Ingress controller set up in your cluster.
    * To check whether you have an Ingress controller set up in your Kubernetes cluster, you can follow these steps:
    ```markdown
    kubectl get pods -n kube-system
    ```
    * If ingress controller is not installed. Follow below steps:
        * Run the following commands to download the necessary manifest files for the Nginx Ingress Controller:
        ````markdown
         wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud/deploy.yaml
        ````
        * Run the following command to apply the downloaded manifest file:
        ````markdown
        kubectl apply -f deploy.yaml
        ````

## Custom Resource Definition (CRD) Configuration
Custom Resource Definitions (CRDs) in Kubernetes allow you to define your own custom resources and their schemas. Let's walk through a complete example of how to create a CRD and use it to create custom resources.

### Create the Custom Resource Definition (crd.yaml):
  First, you need to define the structure of your custom resource by creating a Custom Resource Definition.

```yml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: myapps.example.com
spec:
  group: example.com
  version: v1
  scope: Namespaced
  names:
    plural: myapps
    singular: myapp
    kind: MyApp
    shortNames:
    - ma
```
In this example, we're creating a CRD named `myapps.example.com`. The CRD specifies the `group`, `version`, `scope`, and naming for the custom resource. This CRD defines a `MyApp` resource.

Apply the CRD using:

```markdown
kubectl apply -f crd.yaml
```

### Create the Custom Resource (myapp.yaml):

Now, you can create a custom resource of the type defined in the CRD.

```yml
apiVersion: example.com/v1
kind: MyApp
metadata:
  name: myapp-sample
spec:
  size: Medium
```

In this example, we're creating a `MyApp` resource named `myapp-sample` with a `spec` field indicating the size as "Medium". The `example.com/v1` API version matches the `group` and `version` specified in the CRD.

Apply the custom resource using:
```markdown
kubectl apply -f myapp.yaml
```

### View and Interact with the Custom Resource:
You can use the following commands to view and interact with your custom resource:
* View all instances of the custom resource:
```markdown
kubectl get myapps
```
* View details of a specific custom resource instance:
```markdown
kubectl get myapp myapp-sample -o yaml
```

### Clean Up:
To remove the custom resource and CRD, delete them using:

```markdown
kubectl delete -f myapp.yaml
kubectl delete -f crd.yaml
```
The process involves defining a CRD to specify the structure of your custom resource and then creating instances of that custom resource based on the CRD's schema. This allows you to extend Kubernetes with your own domain-specific resources and manage them using the Kubernetes API. Remember that Custom Resource Definitions are useful for creating higher-level abstractions and encapsulating custom application logic within your Kubernetes cluster.

## Job and CronJob Configuration:
Here's a complete example of how to configure a Job and a CronJob in Kubernetes:

### 1. Job Configuration (job.yaml):
A Job in Kubernetes is used to run a certain task to completion, ensuring that the task runs to completion and is not restarted.

```yml
apiVersion: batch/v1
kind: Job
metadata:
  name: my-job
spec:
  template:
    spec:
      containers:
        - name: my-container
          image: busybox
          command: ["echo", "Hello from the job!"]
      restartPolicy: Never
  backoffLimit: 4
```
In this example, we're creating a Job named `my-job`. The Job will run a container using the `busybox` image and execute the `echo` command. The `restartPolicy` is set to `Never` to ensure the job is not restarted on failure. The `backoffLimit` indicates the number of times the Job should be retried before it's considered failed.

Apply the Job using:

```markdown
kubectl apply -f job.yaml
```

### 2. CronJob Configuration (cronjob.yaml):
A CronJob in Kubernetes is used to schedule jobs to run at specific times, similar to the Unix cron syntax.

```yml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: my-cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: my-container
            image: busybox
            command: ["echo", "Hello from the cron job!"]
          restartPolicy: Never
  successfulJobsHistoryLimit: 3
  failedJobsHistoryLimit: 1
```
In this example, we're creating a CronJob named `my-cronjob`. The CronJob is scheduled to run every minute (`"*/1 * * * *"`). It uses a similar template structure as the Job. The `successfulJobsHistoryLimit` and `failedJobsHistoryLimit` indicate how many completed and failed jobs to keep.

Apply the CronJob using:

```markdown
kubectl apply -f cronjob.yaml
```

### 3. Viewing Job and CronJob Status:
You can view the status of a Job using:
```markdown
kubectl describe job my-job
```
Similarly, you can view the status of a CronJob using:

```markdown
kubectl describe cronjob my-cronjob
```

Remember that Jobs run once to completion, while CronJobs are scheduled to run at specific intervals. The examples provided use basic commands like `echo`, but you can replace them with more complex tasks or application-specific actions.


























































   







































