```
 522  cd k8s-adv-vmware-26-Sept-2022/
  523  ls
  524  docker ps
  525  docker logs b9cc61e05f85
  526  docker logs -f b9cc61e05f85
  527  kubectl  get pods
  528  kubectl  get pods -n kube-system
  529  kubectl  logs pods  kube-apiserver-master -n kube-system
  530  kubectl  logs   kube-apiserver-master -n kube-system
  531  kubectl  logs  -f  kube-apiserver-master -n kube-system
  532  ls
  533  mkdir 15-Metric-Server
  534  ls
  535  cd 15-Metric-Server/
  536  ls
  537  vim metric-server.yaml
  538  ls
  539  kubectl  apply -f metric-server.yaml
  540  kubectl  get pods
  541  kubectl  get pods -n kube-system
  542  kubectl top
  543  kubectl top nodes
  544  kubectl top pods
  545  kubectl top pods -n kube-system
```
