Task:
Run a Docker Ghost deployment which runs on port 2368, expose it as a service and port forward it on your PC. Show the logs as well.


Solution:

kubectl run ghost --image ghost --restart=Always --port 2368 --dry-run -o yaml > deployment-ghost.yaml

kubectl expose deploy/ghost --target-port 2368 --port 80 --type ClusterIP --dry-run -o yaml > service-ghost.yaml

kubectl port-forward svc/ghost 8080:80

kubectl logs <pod-name> -f

Cleanup: 

kubectl delete deploy ghost
kubectl delete svc ghost