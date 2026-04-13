# Kubernetes

```
minikube start --extra-config="apiserver.cors-allowed-origins=['http://boot.dev']"
minikube dashboard --port=63840
local dashboard for the cluster
http://127.0.0.1:63840/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default
```


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
A replicaset is what mantains the desired number of pods running
`kubectl get replicasets`

Config:
`kubectl get deployment synergychat-web -o yaml > web-deployment.yaml`
edit and apply changes:
`kubectl apply -f web-deployment.yaml`

Trashing pods:
* The application recently had a bug introduced in the latest image version
* The application is misconfigured and can't start properly
* A dependency of the application is misconfigured and the application can't start properly
* The application is trying to use too much memory and is being killed by Kubernetes


## ConfigMaps
The way to manage envs 

`kubectl get configmaps`


### Crawler

```
kubectl apply -f crawler-configmap.yaml`
```


## Service
by default clusterIP 

nodePort 
```
kubectl get svc
kubectl proxy
```

The Gateway object not only exposes your service to the outside world, but also allows you to do things like:

- Host multiple services on the same IP address
- Host multiple services on the same port (path-based routing)
- Terminate SSL
- Integrate directly with external DNS and load balancers

Gateway is the new alternative of Ingress
Let's use Envoy Gateway
```
kubectl apply --server-side -f https://github.com/envoyproxy/gateway/releases/download/v1.5.1/install.yaml

kubectl get gateway
kubectl get httproute
```
synchat.internal to the web-service
synchatapi.internal to the api-service


/etc/hosts
127.0.0.1        synchat.internal
127.0.0.1        synchatapi.internal


```
minikube tunnel -c
minikube tunnel --bind-address="127.0.0.1" -c


kubectl get deployment synergychat-web -o yaml | grep -A 5 envFrom
```


## Volumes
The Kubernetes volume abstraction solves two primary problems:

    Data persistence
    Data sharing across containers


## PV and PVC
PVs can be created statically or dynamically.

* Static PVs are created manually by a cluster admin
* Dynamic PVs are created automatically when a pod requests a volume that doesn't exist yet

A persistent volume claim is a request for a persistent volume. When using dynamic provisioning, a PVC will automatically create a PV if one doesn't exist that matches the claim.

```
kubectl get pvc
kubectl get pv
```


# Namespaces
```
kubectl -n kube-system get pod

kubectl create ns crawler
kubectl get ns
```