```
220  cd 10-Labels/
  221  ls
  222  kubectl get pods
  223  vim 01-Helloworld-deploy.yaml
  224  cat 01-Helloworld-deploy.yaml
  225  kubectl  apply -f 01-Helloworld-deploy.yaml
  226  kubectl  describe pod helloworld-deployment-9bb9467cc-7wbxt
  227  kubectl  get nodes
  228  kubectl  get nodes --show-labels
  229  kubectl label node worker2 hardware=virtual
  230  kubectl  get nodes --show-labels
  231  kubectl  scale --replicas=5 -f 01-Helloworld-deploy.yaml
  232  kubectl  scale --replicas=1 -f 01-Helloworld-deploy.yaml
  233  kubectl  scale --replicas=2 -f 01-Helloworld-deploy.yaml
  234  kubectl label node worker1 hardware=virtual
  235  kubectl  get nodes --show-labels
  236  kubectl  scale --replicas=3 -f 01-Helloworld-deploy.yaml
  237  ls
  238  vim 02-Helloworld-deploy-multi-label.yaml
  239  kubectl  apply -f 02-Helloworld-deploy-multi-label.yaml
  240  cat 02-Helloworld-deploy-multi-label.yaml
  241  kubectl label node worker1 env=prod
  242  kubectl label node worker1 hardware-
  243  kubectl label node worker1 env-
  244  kubectl  get nodes --show-labels
  245  kubectl  delete pod helloworld-deployment-2-56bd98d4cb-hwzgp
```
