
### Run node-prerequisites.sh on all of the master VMs


### On the master nodes, Open the following ports
```
firewall-cmd --permanent --add-port=6443/tcp
firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10251/tcp
firewall-cmd --permanent --add-port=10252/tcp
firewall-cmd --permanent --add-port=10255/tcp
firewall-cmd --permanent --add-port=8472/udp
firewall-cmd --add-masquerade --permanent
firewall-cmd --permanent --add-port=30000-32767/tcp
```

```systemctl restart firewalld```

 
 ### Create Default Audit Policy
```
mkdir -p /etc/kubernetes
cat > /etc/kubernetes/audit-policy.yaml <<EOF
apiVersion: audit.k8s.io/v1beta1
kind: Policy
rules:
- level: Metadata
EOF
```

```mkdir -p /var/log/kubernetes/audit```

### setup the initial master

copy kubeadm-config.yaml to a file called kubeadm-config.yaml in your first master

```kubeadm init --config kubeadm-config.yaml --upload-certs```