## Get kubernetes system pods
```
  kubectl get pods -n kube-system
  cd  /etc/kubernetes/manifests/
  vim kube-apiserver.yaml
  kubectl cluster-info
  kubectl version
  kubectl api-versions
  kubectl api-resources
  curl -k https://172.31.0.100:6443
  kubectl proxy --address='172.31.0.100' --port=8080 --accept-hosts='.' --accept-paths='.' &
  curl  http://172.31.0.100:8080
  curl  http://172.31.0.100:8080/api
  kubectl  get pods
  cd .kube/
  kubectl config view
  kubectl config get-contexts
```
