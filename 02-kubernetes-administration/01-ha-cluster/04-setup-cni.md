## Available CNIs

### Flannel

Software based L2-L3 Router. Doesn't support kubernetes network policies. Unencrypted

### Calico

Widely used. Uses IPTables. Uses BGP to sync routes. IP Tables can be a bottleneck when large number of services are running in the cluster. Supports Kubernetes Network Policies. Unencrypted

### Waevenet

Encrypted. Supports Kubernetes network policies. Slow performance due to encryption

### Canal

Mix between calico and flannel. Discontinued.

### Cillium

Uses kernel level routing. (BPF). Doesn't use ip tables so supports large number of services without a performance degrade. Fairly new (as of 2019)


### Setup CNI in the cluster

checkout the cni plugins at https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

we will use Calico in this example


``` wget https://docs.projectcalico.org/v3.8/manifests/calico.yaml```

edit calico.yaml file and change the default 192.168.0.0/16 subnet range to the subnet range you specified in kubeadm-config.yaml networking.podSubnet

```kubectl apply -f calico.yaml```

```kubectl get nodes```

nodes should be in a ready state after a while.



### Tests

```kubectl run nginx --image nginx --restart Always --port 80 -o yaml --dry-run > nginx-deploy.yaml```
change the nodename to worker-1 name

```kubectl expose deploy nginx --port 80 --target-port 80 --type ClusterIP```

```kubectl run busybox --image busybox:1.27 --restart Always --dry-run -o yaml > busybox-deploy.yaml```
change the nodename to worker-2 name

apply the 2 files

ssh into busybox using
```kubectl exec -it <busybox-pod-name> -- /bin/sh```

Run the following commands

```
nslookup nginx.default.svc

nslookup google.com

wget nginx.default.svc
```

If all of these get resolved successfully, you are good to go.