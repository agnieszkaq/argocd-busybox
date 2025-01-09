# Kubernetes GitOps Deployment with Helm for Spring-Boot API

## General info 
This project uses Kubernetes for managing containers, Argo CD for automating deployments, and Helm for managing application settings. It deploys and scales a Spring-Boot API, using Helm to handle configurations for different environments and Argo CD to manage the deployment process.

### Versions
* Kubernetes v1.31.0
* ArgoCD v2.8.0
* Helm v3.14.2 

### Commands to Set Up Environment on Ubuntu
```
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64/
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
minikube start
kubectl config current-context
kubectl apply -k https://github.com/argoproj/argo-cd/manifests/crds\?ref\=stable
kubectl apply -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl port-forward svc/argocd-server 8080:80
localhost:8080
kubectl  get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
helm create spring-boot-api
```

#### Deploy ApplicationSet on ArgoCD 
Before deploying the ApplicationSet, configure two clusters within the application: 
* ```dev-global-cluster-0```
* ```prd-global-cluster-5```

Then, apply the ApplicationSet manifest:
```
kubectl apply -f appset.yaml 
```

### Configuration Values 
Values are stored in the following repository:
* https://github.com/agnieszkaq/values.git