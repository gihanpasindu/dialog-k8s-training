
  kubectl get pods -n nginx-ingress
  kubectl get svc -n nginx-ingress
  kubectl expose deploy/nginx --port 80 --target-port 80
  kubectl expose deploy/nginx --port 80 --target-port 80 --type ClusterIP
 
  kubectl get ing

  curl  --header 'Host: nginx.dialog.com ' http://104.197.127.107

  kubectl get svc --all-namespaces
  kubectl get ing --all-namespaces