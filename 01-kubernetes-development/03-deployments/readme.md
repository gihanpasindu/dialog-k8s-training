 kubectl run nginx --image nginx --dry-run --port 80 --restart=Always -o yaml > deployment-nginx.yaml

 kubectl run nginx --image nginx --dry-run --port 80 --restart=Never -o yaml > pod-nginx.yaml
 
 kubectl apply -f deployment-nginx.yaml 
 kubectl get deploy     

 kubectl describe deploy nginx
 kubectl rollout history deploy/nginx
 kubectl rollout undo deploy/nginx --to-revision=2
 kubectl rollout pause deploy/nginx
 kubectl delete deploy nginx
 kubectl delete pod nginx --force --grace-period=0