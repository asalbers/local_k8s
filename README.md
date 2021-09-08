# local_k8s

## Kind 

### Installation

Kind works on MacOS, Linux and Windows. 

[Installation Docs](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

### Creating cluster

You need to create the Kind cluster before running deployments against it. WSL2 requires the cluster-config to be passed in order to access it externally.

```sh
 kind create cluster --name aa-test --config=kind-cluster-config.yaml # if name left blank defaults to kind
```
### Deploying a workload

Load an image on the cluster

```sh
kind load docker-image test-dotnet:latest --name aa-test
```
Apply the manifest to the cluster

```sh
kubectl apply -f manifests/deployment-dotnet-simple.yaml --context kind-aa-test

kubectl get pods --context kind-<cluster name>
```

Describing the pod

```sh
kubectl describe pod <pod name> --context kind-<cluster name>
```
Clean up

```sh
kubectl delete -f manifests/deployment-dotnet-simple.yaml
```

nginx example

```sh
kubectl apply -f manifests/deployment-nginx.yaml --context kind-<cluster name>

kubectl get pods --context kind-<cluster name>

kubectl describe pod <pod name> --context kind-<cluster name>
kubectl delete -f manifests/deployment-nginx.yaml 

curl http://localhost:30000/ # or go to the web page in browser
```


### Deleting a Cluster

```sh
kind delete cluster --name aa-test # if left blank defaults to kind
```

### Additional Kind docs

[Ingress](https://kind.sigs.k8s.io/docs/user/ingress/)

[Private Registries](https://kind.sigs.k8s.io/docs/user/private-registries/)

[WSL2](https://kind.sigs.k8s.io/docs/user/using-wsl2/)

[load balancer](https://kind.sigs.k8s.io/docs/user/loadbalancer/)

## Minikube

### Installation

Works on MacOS, Linux and Windows.

[Installation](https://minikube.sigs.k8s.io/docs/start/)

### Creating a Cluster

```sh
minikube start
```

### Deploying a workload

Loading a local image

```sh
minikube image load test-dotnet:1.0.0
```

Apply the manifest to the cluster

```sh
kubectl apply -f local_k8s/manifests/deployment-dotnet-simple.yaml --context kind-aa-test

kubectl get pods --context kind-aa-test
```

Describing the pod

```sh
kubectl describe pod simple-dotnet-bf85f5cc4-5vh79 --context kind-aa-test
```

Clean up

```sh
kubectl delete -f local_k8s/manifests/deployment-dotnet-simple.yaml
```

Nginx example

```sh
kubectl apply -f manifests/deployment-nginx.yaml 

kubectl get pods 

kubectl describe pod <pod name> 
kubectl delete -f manifests/deployment-nginx.yaml 

curl http://localhost:30000/ # or go to the web page in browser
```

### Deleting a Cluster 

```sh
minikube delete --all # will delete all minikube clusters
```