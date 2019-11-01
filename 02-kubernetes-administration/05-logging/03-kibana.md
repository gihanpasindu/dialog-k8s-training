helm install --name kibana elastic/kibana
 kubectl port-forward svc/kibana-kibana    5601