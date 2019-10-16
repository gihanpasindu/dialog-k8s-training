 kubectl run busybox --image busybox -o yaml --restart Never --dry-run > pod-empty-dir.yaml

  kubectl run busybox --image busybox -o yaml --restart Never --dry-run > pod-host-path.yaml