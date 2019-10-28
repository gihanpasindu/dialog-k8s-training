kubectl run nginx --image nginx  --port 80 --restart=Always

kubectl expose deploy/nginx --port 80 --target-port 80 --dry-run -o  yaml  --type=ClusterIP > service-nginx.yaml

kubectl apply -f service-nginx.yaml

kubectl get svc

kubectl port-forward svc/nginx 3000:80

kubectl run busybox --image busybox:1.27 -it --rm -- /bin/sh

<service-name>.<namespace>.svc.cluster.local

