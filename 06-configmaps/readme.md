kubectl delete pods --all

kubectl run busybox --restart=Always --dry-run --image busybox -o yaml > deployment-busybox.yaml

kubectl exec -it <pod-name> -- /bin/sh

kubectl exec -it <pod-name> -- env   

kubectl create configmap literal-config --from-literal=ENV=DEV --from-literal=company=dialog --dry-run -o yaml > configmap-dialog.yaml

kubectl create configmap file-config --from-file=.properties --dry-run -o yaml > configmap-from-file.yaml