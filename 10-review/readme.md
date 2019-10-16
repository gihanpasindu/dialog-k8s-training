Create a deployment for Nextcloud https://hub.docker.com/_/nextcloud
Open the port 80
Create 2 PVCs for 1GB using GCP Persistent Disks and name them html and db
Mount the 2 PVCs to the pods on the paths /var/www/html and /var/lib/mysql

Make sure the deployment only has 1 replica

expose the deployment as a service. 

Save up all the yamls



Solution:

kubectl run nextcloud --image nextcloud --port 80 -o yaml --dry-run > deployment-nextcloud.yaml

kubectl expose deploy/nextcloud --port 80 --target-port 80 --type ClusterIP --dry-run -o yaml > service-nextcloud.yaml

kubectl port-forward svc/nextcloud 8080:80