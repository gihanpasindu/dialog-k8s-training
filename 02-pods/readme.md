kubectl get nodes
kubectl get ns
kubectl get pods -n kube-system
kubectl create ns dialog
kubectl run nginx --image nginx --restart=Never --port 80 -n dialog
kubectl get pods -n dialog

set up a kubectl
https://medium.com/free-code-camp/how-to-set-up-a-serious-kubernetes-terminal-dd07cab51cd4

kubectl port-forward po/nginx 8080:80 -n dialog
kubectl exec -it -n dialog  nginx -- /bin/sh 
kubectl get pods --all-namespaces
kubectl delete pod nginx -n dialog
kubectl run nginx --image nginx --restart=Never --port 80 -n dialog --dry-run -o yaml > nginx-pod.yaml
kubectl explain Pod.spec.containers.ports
kubectl apply -f nginx-pod.yaml 