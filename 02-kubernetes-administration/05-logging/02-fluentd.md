## add repo
helm repo add kiwigrid https://kiwigrid.github.io

helm install --name fluentd kiwigrid/fluentd-elasticsearch --namespace logging --set elasticsearch.host=elasticsearch-master


NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=logging get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.