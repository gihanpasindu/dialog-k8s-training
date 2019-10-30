### Install Helm Client

```
curl -LO https://git.io/get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```
ln -s /usr/local/bin/helm /usr/bin

helm init

kubectl create serviceaccount --namespace kube-system tiller

kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller

kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'

helm init --service-account tiller --upgrade


## Metrics Server

kubectl create ns monitoring

helm install --name metrics-server stable/metrics-server --namespace monitoring \
--set "args[0]=--logtostderr,args[1]=--kubelet-preferred-address-types=InternalIP,args[2]=--kubelet-insecure-tls" 

## Kubernetes Dashbaord

helm install --name kubernetes-dashboard stable/kubernetes-dashboard \
--set rbac.clusterAdminRole=true --namespace kube-system

Get the Kubernetes Dashboard URL by running:
  export POD_NAME=$(kubectl get pods -n kube-system -l "app=kubernetes-dashboard,release=kubern
etes-dashboard" -o jsonpath="{.items[0].metadata.name}")
  echo https://127.0.0.1:8443/
  kubectl -n kube-system port-forward $POD_NAME 8443:8443


  ### nginx ingress

helm install --name nginx-ingress stable/nginx-ingress --namespace nginx-ingress  \
--set rbac.create=true \
--set controller.service.type=NodePort \
--set controller.metrics.enabled=true \
--set controller.stats.enabled=true 

  An example Ingress that makes use of the controller:
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls
If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be pro
vided:
  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls



  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: nignx
  spec:
    rules:
      - host: nginx.com
        http:
          paths:
            - backend:
                serviceName: nignx
                servicePort: 80
              path: /