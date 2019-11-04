helm install --namespace logging --name graylog stable/graylog --values graylog-values.yaml


Variables
Ingress host
Elasticsearch Host URL (If you have elasticsearch seperately)
Inputs - to configure multiple expose ports


NOTES:
To connect to your Graylog server:

1. Get the application URL by running these commands:
  http://graylog.kubernetes.lk

2. The Graylog root users

  echo "User: admin"
  echo "Password: $(kubectl get secret --namespace logging graylog -o "jsonpath={.data['graylog-password-secret']}" | base64 --decode)"

To send logs to graylog:

  NOTE: If `graylog.input` is empty, you cannot send logs from other services. Please make sure the value is not empty.
        See https://github.com/helm/charts/tree/master/stable/graylog#input for detail
2. UDP
  export POD_NAME=$(kubectl get pods --namespace logging -l "app.kubernetes.io/name=graylog,app.kubernetes.io/instance=graylog" -o jsonpath="{.items[0].metadata.name}")
  Run the command
  kubectl port-forward $POD_NAME 12201:12201
  Then send logs to 127.0.0.1:12201