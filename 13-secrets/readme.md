kubectl create secret generic  literal-secret --from-literal=ENV=DEV --from-literal=company=dialog --dry-run -o yaml > secret-literal.yaml


helm install stable/kubernetes-dashboard --name dashboard --namespace kube-system --set rbac.clusterAdminRole=true 


NOTES:
*********************************************************************************
*** PLEASE BE PATIENT: kubernetes-dashboard may take a few minutes to install ***
*********************************************************************************

Get the Kubernetes Dashboard URL by running:
  export POD_NAME=$(kubectl get pods -n kube-system -l "app=kubernetes-dashboard,release=dashboard" -o jsonpath="{.items[0].metadata.name}")
  echo https://127.0.0.1:8443/
  kubectl -n kube-system port-forward $POD_NAME 8443:8443