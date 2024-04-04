---
layout: default
title: Helm Chart
parent: Kubernetes
nav_order: 7
---
# Helm Chart
Helm is a package manager for Kubernetes that simplifies the deployment and management of applications and services on a Kubernetes cluster. Helm uses a concept called "charts" to package Kubernetes resources, making it easier to define, install, and upgrade complex applications.

Here's a breakdown of what a Helm chart is:

1. Package Format: A Helm chart is a collection of Kubernetes manifest files (YAML files) packaged together into a single compressed archive. This archive contains all the resources needed to deploy a specific application or service on a Kubernetes cluster.
2. Templates and Values: Helm charts include templates that allow you to parameterize Kubernetes resource definitions using placeholders, such as `{{ .Values.someValue }}`. These placeholders are replaced with actual values when you install or upgrade the chart. Values are typically stored in a separate file called `values.yaml`, allowing for easy customization of the chart.
3. Versioning: Helm charts can have version numbers, making it possible to track and manage different versions of an application or service. This versioning simplifies rollbacks and ensures consistency in deployments.
4. Dependencies: Helm charts can also declare dependencies on other charts. This feature allows you to define complex applications composed of multiple components, each managed by its own chart. Helm can automatically resolve and install these dependencies.
5. Release Management: Helm keeps track of releases, which are specific instances of a chart deployed on a cluster. Each release can have its own configuration values, allowing you to manage multiple instances of the same application with different settings.
6. Hooks: Helm charts can include lifecycle hooks that run at specific points during installation or upgrading. These hooks enable you to perform actions like database migrations, secret generation, or configuration updates as part of the deployment process.
7. Repository: Helm charts are typically distributed via chart repositories, which are similar to package repositories. Helm repositories provide a convenient way to share, discover, and distribute charts within an organization or to the broader community.

Here's an example use case to illustrate the utility of Helm charts:

Example: Deploying a WordPress Application

Let's say you want to deploy a WordPress application on your Kubernetes cluster. With Helm, you can use a pre-existing WordPress Helm chart, or you can create a custom chart for your specific needs. The chart might include templates for defining Kubernetes resources such as Deployments, Services, ConfigMaps, and Secrets for WordPress and its database backend.

You can customize values in the `values.yaml` file to specify database credentials, WordPress configuration, and other settings. When you're ready to deploy, you can use Helm to install the chart, and Helm will generate the necessary Kubernetes resources based on the templates and values you've provided.

Helm simplifies the deployment and management of WordPress and allows you to easily upgrade to new versions, rollback to previous versions, or uninstall the application cleanly.

In summary, Helm charts are a powerful tool for packaging, deploying, and managing complex applications and services on Kubernetes clusters, making it easier to work with Kubernetes resources in a more modular and repeatable manner.

## Install Helm: 
You should also install Helm on your macOS if it's not already installed. You can use Homebrew for this as well:
```markdown
brew install helm
```
* Add Helm Repository (Optional): If the Helm chart you want to install is hosted in a Helm chart repository, you can add the repository to Helm:
```markdown
helm repo add <repository-name> <repository-url>
```
Replace `<repository-name>` with a suitable name and `<repository-url>` with the URL of the Helm chart repository.
* Search for Helm Charts (Optional): You can search for available Helm charts in the repository using:
```markdown
helm search repo <repository-name>
```
* Install the Helm Chart: Use the `helm install` command to install the Helm chart on your Minikube cluster. You'll need to specify the chart name and optionally provide a release name and set values:
```markdown
helm install <release-name> <chart-name> [flags] --set key1=value1,key2=value2,...
```
* `<release-name>` is the name you want to give to this specific installation of the chart.
* `<chart-name>` is the name of the Helm chart you want to install.
* `[flags]` can include additional configuration options.
* `--set` is used to provide custom configuration values.

### Example:
```markdown
helm install my-wordpress stable/wordpress --set service.type=NodePort
```

## Here's a list of some common Helm commands
* helm create: Create a new chart template with the given name.
```markdown
helm create mychart
```

* helm install: Install a Helm chart onto your Kubernetes cluster.
```markdown
helm install <release-name> <chart-name> [flags] --set key1=value1,key2=value2,...
```

* helm list: List all releases installed in your cluster.
```markdown
helm list [flags]
```

* helm status: Display the status of a release.
```markdown
helm status <release-name>
```

* helm upgrade: Upgrade a release to a new version of a chart.
```markdown
helm upgrade <release-name> <chart-name> [flags] --set key1=value1,key2=value2,...
```

* helm rollback: Rollback to a previous version of a release.
```markdown
helm rollback <release-name> <revision>
```

* helm uninstall: Uninstall a release from your cluster.
```markdown
helm uninstall <release-name>
```

* helm package: Package a chart into a versioned chart archive.
```markdown
helm package <chart-directory>
```

* helm repo add: Add a Helm chart repository to your Helm installation.
```markdown
helm repo add <repository-name> <repository-url>
```

* helm repo list: List all Helm chart repositories added to Helm.
```markdown
helm repo list
```

* helm repo update: Update the local cache of Helm chart repositories.
```markdown
helm repo update
```

* helm dependency update: Update the dependencies of a chart.
```markdown
helm dependency update <chart-directory>
```

* helm lint: Check a chart for issues.
```markdown
helm lint <chart-directory>
```

* helm template: Render a chart locally as Kubernetes manifest files without installing it.
```markdown
helm template <release-name> <chart-name> [flags] --set key1=value1,key2=value2,...
```

* helm get values: Show the values used in a release.
```markdown
helm get values <release-name>
```

* helm history: View release history, including revisions and timestamps.
```markdown
helm history <release-name>
```

* helm show chart: Show chart information such as the chart's README.
```markdown
helm show chart <chart-name>
```

* helm show values: Show the default values for a chart.
```markdown
helm show values <chart-name>
```

* helm show all: Show all information about a chart.
```markdown
helm show all <chart-name>
```

* helm plugin install: Install a Helm plugin.
```markdown
helm plugin install <plugin-name>
```

---
# Example for our previous api-caller application
In our previous example, we deployed a full-fledged application in the minikube Kubernetes cluster. Now, we are creating a helm chart for this application.

## Directory Structure:
```markdown
api-caller-helm-chart/
  Chart.yaml
  values.yaml
  templates/
    backend-scaling.yaml
    front-end.yaml
    ingress.yaml
    namespaces.yaml
    service1-config.yaml
    service1.yaml
    service2.yaml
```
Here's the content of each file:
### Chart.yaml:
```yml
apiVersion: v2
name: my-helm-chart
description: A Helm chart for your Kubernetes resources
version: 0.1.0
```

### values.yaml:
```yml
# You can define default values for your resources here if needed.
```
### templates/backend-scaling.yaml:
```yml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: backend-scaling-service1
  namespace: my-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: service1-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 10
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: backend-scaling-service2
  namespace: my-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: service2-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
    - type: Resource
      resource:
        name: memory
        target:
          type: Utilization
          averageUtilization: 70
```
### templates/front-end.yaml:
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
  type: LoadBalancer
```
### templates/ingress.yaml:
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
### templates/namespaces.yaml:
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: my-app
---
apiVersion: v1
kind: Namespace
metadata:
  name: my-app-2
```
### templates/service1-config.yaml:
```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: service1-config
  namespace: my-app
data:
  SERVICE_2_API_URL: "http://service2-service.my-app-2.svc.cluster.local:8080"
```

### templates/service1.yaml:
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
          envFrom:
            - configMapRef:
                name: service1-config  # Reference the ConfigMap here
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

### templates/service2.yaml:
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

With this structure, you have organized your resources into separate files, and you can create the Helm chart by packaging the `api-caller-helm-chart/` directory:

```markdown
helm package api-caller-helm-chart/
```
The following file will be created:
```markdown
api-caller-helm-chart-0.1.0.tgz
```
Then, you can install this Helm chart with `helm install` and customize the values as needed.

## Install api-caller into Kubernetes
```markdown
helm install my-api-caller api-caller-helm-chart-0.1.0.tgz

NAME: my-api-caller
LAST DEPLOYED: Tue Sep  5 12:36:39 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

### Executing helm command
* helm status <release-name>
```markdown
helm status my-api-caller

NAME: my-api-caller
LAST DEPLOYED: Tue Sep  5 12:36:39 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

```markdown
helm uninstall my-api-caller
release "my-api-caller" uninstalled
```
---
let's consolidate the Kubernetes resources into a single deployment file, a single service file, a single namespace file, and a single Horizontal Pod Autoscaler (HPA) file while parameterizing the configuration using Helm values. We'll also make use of Helm's templating capabilities to achieve this.

Here's an optimized structure for your Helm chart:

```markdown
my-helm-chart/
  Chart.yaml
  values.yaml
  templates/
    all-in-one.yaml
```
* Chart.yml:
```yml
apiVersion: v2
  name: my-helm-chart
  description: A Helm chart for deploying and scaling resources.
  version: 0.1.0
```
* values.yaml:
```yml
# Default values for your Helm chart
app:
  name: my-app
  version: 1.0.0

resources:
  cpuLimit: "200m"
  memoryLimit: "256Mi"
service1:
  image: a1anjanjana/service-1:latest
  # ... other service1-specific values

service2:
  image: a1anjanjana/service-2:latest
  # ... other service2-specific values
 
```
* templates/all-in-one.yaml:
```yml
apiVersion: v1
kind: Namespace
metadata:
  name: {{ .Values.app.name }}

--

apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Values.app.name }}-deployment
  namespace: {{ .Release.Namespace }}
spec:
  replicas: 1
  selector:
    matchLabels:
      app: {{ .Values.app.name }}
  template:
    metadata:
      labels:
        app: {{ .Values.app.name }}
    spec:
      containers:
        - name: {{ .Values.app.name }}
          image: {{ .Values.service1.image }}
          # ... other common container settings
          resources:
            requests:
              memory: {{ .Values.resources.memoryLimit }}
              cpu: {{ .Values.resources.cpuLimit }}
            limits:
              memory: {{ .Values.resources.memoryLimit }}
              cpu: {{ .Values.resources.cpuLimit }}
--

apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.app.name }}-service
  namespace: {{ .Release.Namespace }}
spec:
  selector:
    app: {{ .Values.app.name }}
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
--

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: {{ .Values.app.name }}-scaling
  namespace: {{ .Release.Namespace }}
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: {{ .Values.app.name }}-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 10
 
```





















