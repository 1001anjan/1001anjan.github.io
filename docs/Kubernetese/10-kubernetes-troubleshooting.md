---
layout: default
title: Troubleshooting
parent: Kubernetes
nav_order: 10
---
# Troubleshooting 
## Find minikube cluster ip
```markdown
minikube ip
```
## Configure metric-service to view resource utilization
### Deploy metric-service
```markdown
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
### check if service running status
```markdown
kubectl get pods -n kube-system | grep metrics-server  
```
### View pod logs
```markdown
kubectl logs -n kube-system metrics-server-<container>
```
### Fix SSL error
Edit the args section under Deployment:
```yml
spec:
  containers:
  - args:
    - --cert-dir=/tmp
    - --secure-port=443
    - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
    - --kubelet-use-node-status-port
    - --metric-resolution=15s
```
enable insure access by adding following argument to the spec.
```yml
    - --kubelet-insecure-tls=true
```
---
## NodePort access
A NodePort service is the most basic way to get external traffic directly to your service. NodePort, as the name implies, opens a specific port, and any traffic that is sent to this port is forwarded to the service.
### Getting the NodePort using the service command 
```markdown
minikube service <service-name> --url
```
Official Documentation: https://minikube.sigs.k8s.io/docs/handbook/accessing/

