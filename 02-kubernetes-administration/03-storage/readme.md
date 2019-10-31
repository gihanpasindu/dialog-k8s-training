## Openebs

yum install iscsi-initiator-utils -y
systemctl enable iscsid && sudo systemctl start iscsid

kubectl create ns openebs
helm install --namespace openebs --name openebs stable/openebs --version 1.3.0

Now you can see 4 storage classes applied on kubernetes. 
kubectl get sc


NOTES:
The OpenEBS has been installed. Check its status by running:
$ kubectl get pods -n openebs
For dynamically creating OpenEBS Volumes, you can either create a new StorageClass or use one of the default storage classes provided by OpenEBS.
Use `kubectl get sc` to see the list of installed OpenEBS StorageClasses. A sample PVC spec using `openebs-jiva-default` StorageClass is given below:
"
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: demo-vol-claim
spec:
  storageClassName: openebs-jiva-default
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5G
---
For more information, please visit http://docs.openebs.io/.
Please note that, OpenEBS uses iSCSI for connecting applications w
ith the
OpenEBS Volumes and your nodes should have the iSCSI initiator ins
talled.