## OFFICIAL  elasticsearch repo
helm repo add elastic https://helm.elastic.co

Create namespace


kubectl create ns logging

helm install --name elasticsearch elastic/elasticsearch

## change values of values.yaml as an when needed here
https://github.com/elastic/helm-charts/tree/master/elasticsearch

NOTES:
1. Watch all cluster members come up.
  $ kubectl get pods --namespace=logging -l app=elasticsearch-master -w
2. Test cluster health using Helm test.
  $ helm test elasticsearch