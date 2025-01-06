# argocd-busybox
K8S, ArgoCD, HELM


### Versions
* Kubernetes v1.31.0
* ArgoCD v2.8.0
* Helm v3.14.2 

### Used command to set up environment

##### terminal
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

#### Deploy ApplicationSet on argocd 
```
kubectl apply -f appset.yaml 
```

#### Values are stored in https://github.com/agnieszkaq/values.git