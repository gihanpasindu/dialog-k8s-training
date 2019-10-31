kubectl create ns monitoring

helm install stable/prometheus-operator --name prom-operator --values values.yaml --namespace monitoring

things you should consider changing

storage class
storage size
retention period

### only on GKE
kubectl delete ValidatingWebhookConfiguration --all
kubectl delete MutatingWebhookConfiguration --all



grafana default credentials
un= admin
pw= prom-operator