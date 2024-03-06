---
layout: default
title: Minikube & kubectl
parent: Kubernetes
nav_order: 2
---
# Minikube
Minikube is a tool that enables you to run a single-node Kubernetes cluster locally on your computer. It's designed to provide a simple and lightweight way to develop and test applications using Kubernetes without the need for a full-scale production cluster. Minikube creates a virtual machine (VM) on your local system and installs a Kubernetes cluster within that VM.

Key features and purposes of Minikube include:
* Local Kubernetes Development: Minikube allows developers to set up and experiment with Kubernetes without needing access to a cloud-based or remote Kubernetes cluster. This is especially useful for testing and developing applications.
* Isolated Environment: Minikube provides an isolated environment in which you can deploy and test applications as if they were running in a real Kubernetes cluster.
* Single-Node Cluster: Minikube creates a single-node Kubernetes cluster on your local machine. While it doesn't provide the full scaling capabilities of a multi-node cluster, it offers most of Kubernetes' core features.
* Kubernetes Versions: Minikube supports different versions of Kubernetes, allowing you to test applications against specific versions before deploying them to a production cluster.
* Easy Setup: Minikube abstracts away much of the complexity of setting up a Kubernetes cluster. It can be set up quickly using a single command.
* Add-Ons and Plugins: Minikube offers add-ons and plugins that allow you to easily enable features such as storage, networking, and more.
* Docker Integration: Minikube can be used with a Docker daemon within the VM, allowing you to build and push Docker images directly from your local machine to the Minikube cluster.
* Integration with Tools: It integrates well with tools like kubectl (Kubernetes command-line tool) and Docker, making it easy to manage and interact with the local cluster.

Minikube is especially valuable for developers who want to learn, experiment, and develop applications for Kubernetes in a controlled and local environment. It's important to note that while Minikube is great for testing and development, it's not suitable for running production workloads due to its single-node nature and the limited resources available in a local environment.

## kubectl
kubectl is the official command-line tool for interacting with Kubernetes clusters. It serves as the primary interface for managing and controlling Kubernetes resources, such as pods, services, deployments, and more. With kubectl, you can perform various actions on your Kubernetes cluster, including deploying applications, inspecting cluster status, troubleshooting, and managing resources.

Key features and uses of kubectl include:
* Resource Management: kubectl allows you to create, update, delete, and manage various Kubernetes resources. You can define resource configurations using YAML files and apply them to the cluster.
* Cluster Communication: You can use kubectl to communicate with the control plane components of a Kubernetes cluster. It sends commands and requests to the cluster's API server.
* Deployment and Scaling: kubectl enables you to create and manage Deployments, ReplicationControllers, and StatefulSets, allowing you to deploy and scale applications.
* Pod Interaction: You can inspect and interact with individual pods using kubectl. This includes viewing logs, executing commands within pods, and attaching to pod terminals.
* Service Management: kubectl allows you to create and manage Kubernetes services, which enable network connectivity to your pods.
* Configuration Management: You can use kubectl to manage configuration settings for your Kubernetes resources. This includes setting environment variables, resource limits, and more.
* Namespace Management: Kubernetes supports namespaces to provide virtual clusters within a physical cluster. kubectl enables you to work with namespaces, isolating resources and applications.
* Context and Switching: kubectl supports the concept of contexts, allowing you to easily switch between different clusters and user credentials.
* Interacting with Plugins: kubectl can be extended with plugins to provide additional functionality, such as enhanced visualizations, resource management, and more.
* Kubeconfig: kubectl uses a configuration file called kubeconfig that contains information about clusters, users, and contexts. This file is used to authenticate and specify the cluster to interact with.

Overall, kubectl is a powerful tool that simplifies the interaction with Kubernetes clusters, making it accessible to both developers and administrators. It's an essential component for managing and deploying applications in Kubernetes environments.

## Setup minikube
Follow the link : https://minikube.sigs.k8s.io/docs/start/

    
## `kubectl` basic commands
1. kubectl get:
   * List resources (pods, services, deployments, etc.) in a namespace.
   * Example: `kubectl get pods`
2. kubectl describe:
   * Show detailed information about a specific resource.
   * Example: `kubectl describe pod <pod-name>`
3. kubectl create:
   * Create a resource from a file, URL, or stdin.
   * Example: `kubectl create -f deployment.yaml`
4. kubectl apply:
   * Apply changes to a resource using a configuration file.
   * Example: `kubectl apply -f deployment.yaml`
5. kubectl delete:
   * Delete a resource.
   * Example: `kubectl delete pod <pod-name>`
6. kubectl edit:
   * Edit a resource using the default editor.
   * Example: `kubectl edit deployment <deployment-name>`
7. kubectl exec:
   * Execute a command in a running pod.
   * Example: `kubectl exec -it <pod-name> -- /bin/bash`
8. kubectl logs:
   * Print the logs of a pod.
   * Example: `kubectl logs <pod-name>`
9. kubectl port-forward:
   * Forward one or more local ports to a pod.
   * Example: `kubectl port-forward <pod-name> <local-port>:<pod-port>`
10. kubectl get events:
    * Display events related to resources in a namespace.
    * Example: `kubectl get events`
11. kubectl apply -f -:
    * Apply resources from stdin.
    * Example: `cat deployment.yaml | kubectl apply -f -`
12. kubectl scale:
    * Scale the number of replicas in a deployment or replicaset.
    * Example: `kubectl scale deployment <deployment-name> --replicas=<desired-replicas>`
13. kubectl rollout:
    * Manage the rollout of changes to a deployment.
    * Example: `kubectl rollout status deployment <deployment-name>`
14. kubectl get nodes:
    * List the nodes in the cluster.
    * Example: `kubectl get nodes`
15. kubectl get svc:
    * List services in a namespace.
    * Example: `kubectl get svc`
16. kubectl get configmaps:
    * List configmaps in a namespace.
    * Example: `kubectl get configmaps`
17. kubectl apply -k:
    * Apply resources using a Kustomize directory.
    * Example: `kubectl apply -k ./kustomize-dir`
18. kubectl top:
    * Display resource (e.g., pod, node) usage metrics.
    * Example: kubectl top pods
19. kubectl label:
    * Add or update labels on resources.
    * Example: `kubectl label pod <pod-name> app=my-app`
20. kubectl get secrets:
    * List secrets in a namespace.
    * Example: `kubectl get secrets`
21. kubectl rollout undo:
    * Roll back a deployment to a previous revision.
    * Example: `kubectl rollout undo deployment <deployment-name>`
22. kubectl explain:
    * Display documentation for a Kubernetes resource.
    * Example: `kubectl explain pod`

Find more commands and their details in the official Kubernetes documentation or by running `kubectl --help` in your terminal.

---
## Practice set
### Install hyperhit and minikube
    `brew update`
    `brew install hyperkit` //If docker desktop installed then hyperkit is not required to install.
    `brew install minikube`
    `kubectl`
    `minikube`

### create minikube cluster
    `minikube start --vm-driver=hyperkit`
    `kubectl get nodes`
    `minikube status`
    `kubectl version`

#### delete cluster and restart in debug mode
    `minikube delete`
    `minikube start --vm-driver=hyperkit --v=7 --alsologtostderr`
    `minikube status`

### kubectl commands
    `kubectl get nodes`
    `kubectl get pod`
    `kubectl get services`
    `kubectl create deployment nginx-depl --image=nginx`
    `kubectl get deployment`
    `kubectl get replicaset`
    `kubectl edit deployment nginx-depl`

### debugging
    `kubectl logs {pod-name}`
    `kubectl exec -it {pod-name} -- bin/bash`

### create mongo deployment
    `kubectl create deployment mongo-depl --image=mongo`
    `kubectl logs mongo-depl-{pod-name}`
    `kubectl describe pod mongo-depl-{pod-name}`

### delete deployment
    `kubectl delete deployment mongo-depl`
    `kubectl delete deployment nginx-depl`

### create or edit config file
    `vim nginx-deployment.yaml`
    `kubectl apply -f nginx-deployment.yaml`
    `kubectl get pod`
    `kubectl get deployment`

### delete with config
    `kubectl delete -f nginx-deployment.yaml`
### Metrics
kubectl top The `kubectl top` command returns current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified.














 

    

 