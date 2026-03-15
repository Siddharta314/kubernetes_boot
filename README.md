# Kubernetes

`minikube start --extra-config="apiserver.cors-allowed-origins=['http://boot.dev']"`
`minikube dashboard --port=63840`
local dashboard for the cluster
`http://127.0.0.1:63840/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default`


`kubectl create deployment synergychat-web --image=docker.io/bootdotdev/synergychat-web:latest`
deploy container in my local k8s cluster

`kubectl get deployments`

network access is limited, port forwared needed. 
`kubectl get pods`
`kubectl port-forward PODNAME 8080:8080`

## Minikube
Minikube runs a single-node cluster, whereas production clusters are multi-node distributed systems.

Kubernetes manages resources like CPU, memory and disk space required by the application.

## Pods
"Pods are the smallest deployable units of computing that you can create and manage in Kubernetes."

Edit deployment:
`kubectl edit deployment synergychat-web`

Commands: 
```
kubectl logs PODNAME
kubectl delete pod PODNAME
kubectl get pods
kubectl get pods -o wide
kubectl proxy
```


```
Starting to serve on 127.0.0.1:8001
http://127.0.0.1:8001/api/v1/namespaces/default/pods
```

## Deployments
A Deployment provides declarative updates for Pods and ReplicaSets.
```
kubectl get deployment synergychat-web -o yaml
kubectl edit deployment synergychat-web
kubectl get pod
```







