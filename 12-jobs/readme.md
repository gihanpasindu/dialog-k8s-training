kubectl run pi --image=perl --restart=OnFailure -o yaml --dry-run > job-perl.yaml
kubectl apply -f job-perl.yaml

kubectl run hello-hourly --image=busybox --restart=OnFailure --schedule="*/1 * * * *"  -o yaml --dry-run > cronjob-busybox.yaml

https://crontab.guru
