### Create a namespace
It's important you create a namespace with the following label, so that istio can inject it's sidecar proxy to your application

```
kubectl create ns dialog
kubectl label namespace dialog  istio-injection=enabled

kubectl get namespace -L istio-injection

```

### Create 2 deployments for nginx v1 and v2

```
kubectl run nginx-v1 --image nj93/istio-test-svc:v1 --dry-run -o yaml --port 80 --labels 'version=v1,app=nginx' -n dialog > nginx-v1-deployment.yaml

kubectl run nginx-v2 --image nj93/istio-test-svc:v2 --dry-run -o yaml --port 80 --labels 'version=v2,app=nginx' -n dialog > nginx-v2-deployment.yaml
```

``` kubectl get pods --show-labels```


### Create a service common for both of the deployments

```kubectl expose deploy/nginx-v1 --port 80 --target-port 80 --dry-run --type ClusterIP -o yaml > nginx-svc.yaml```


### create a busybox on same namespace to test routing
kubectl run busybox --image busybox:1.27 --restart Never -it -- /bin/sh

wget -O- nginx-svc.dialog.svc

VirtualService ---> DestinationRule ---> Service ---> Pods