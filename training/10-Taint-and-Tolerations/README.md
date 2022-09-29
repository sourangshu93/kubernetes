```
260  mkdir 11-Taint-n-Tolerations
  261  cd 11-Taint-n-Tolerations/
  262  ls
  263  vim 01-helloworld-deploy.yaml
  264  kubectl  apply -f 01-helloworld-deploy.yaml
  265  kubectl  get pods
  266  kubectl  get pods -o wide
  267  kubectl taint node worker1 app=myapp:NoSchedule
  268  kubectl  describe node worker1 | grep -i taint
  269  kubectl  scale --replicas=5 -f 01-helloworld-deploy.yaml
  270  kubectl  scale --replicas=8 -f 01-helloworld-deploy.yaml
  271  kubectl  scale --replicas=3 -f 01-helloworld-deploy.yaml
  272  vim 02-helloworld-deploy-with-toleration.yaml
  273  kubectl  apply -f 02-helloworld-deploy-with-toleration.yaml
  274  kubectl  scale --replicas=6 -f 02-helloworld-deploy-with-toleration.yaml
  275  kubectl delete -f 01-helloworld-deploy.yaml
  276  kubectl delete -f 02-helloworld-deploy-with-toleration.yaml
  277  kubectl  describe node worker1 | grep -i taint
  278  kubectl taint node worker2 example=amit:NoSchedule
  279  kubectl  describe node worker2 | grep -i taint
  280  kubectl  apply -f 01-helloworld-deploy.yaml
  281  kubectl  apply -f 02-helloworld-deploy-with-toleration.yaml
  282  vim 03-helloworld-deploy-with-multi-toleration.yaml
  283  kubectl  apply -f 03-helloworld-deploy-with-multi-toleration.yaml
  284  kubectl taint node worker1 example2=example2-key:NoExecute
  285  vim 04-helloworld-deploy-with-multi-toleration.yaml
  286  kubectl  apply -f 04-helloworld-deploy-with-multi-toleration.yaml
  287  kubectl taint node worker1 example2-
  288  kubectl taint node worker2 example-
  289  kubectl taint node worker1 app-
  290  kubectl taint node worker2 app-
  291  ls
  292  cd ..
  293  ls
  294  kubectl  apply -f 11-Taint-n-Tolerations/
  295  ls
  296  cd 11-Taint-n-Tolerations/
  297  ls
  298  vim 05-helloworld-ds.yaml
  299  kubectl  apply -f 05-helloworld-ds.yaml
  300  cd ..
  301  kubectl  delete -f 11-Taint-n-Tolerations/
  302  kubectl  apply -f 11-Taint-n-Tolerations/05-helloworld-ds.yaml
  303  kubectl  describe nodes master | grep -i taint
  304  kubectl  delete -f 11-Taint-n-Tolerations/05-helloworld-ds.yaml
  305  vim 11-Taint-n-Tolerations/06-helloworld-ds-with-master-toleration.yaml
  306  kubectl  apply -f 11-Taint-n-Tolerations/06-helloworld-ds-with-master-toleration.yaml
  307  kubectl  delete -f 11-Taint-n-Tolerations/06-helloworld-ds-with-master-toleration.yaml
```
