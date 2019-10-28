kubectl autoscale deploy/nginx --cpu-percent=50 --min 1 --max 10 -o yaml --dry-run > hpa-nginx.yaml

kubectl run php-apache --image=k8s.gcr.io/hpa-example --requests=cpu=200m --limits=cpu=500m --expose --port=80

kubectl api-versions