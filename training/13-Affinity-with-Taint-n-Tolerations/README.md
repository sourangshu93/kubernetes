```
 522  cd k8s-adv-vmware-26-Sept-2022/
  523  ping -c2 google.com
  524  ls
  525  mkdir 14-Affinity-with-Taint-n-Tolerations
  526  cd 14-Affinity-with-Taint-n-Tolerations/
  527  vi 01-helloworld.yaml
  528  ls
  529  cat 01-helloworld.yaml
  530  vim 01-helloworld.yaml
  531  kubectl  get nodes
  532  kubectl  get pods
  533  ls
  534  cp -rf ../05-Replication-Cantroller/helloworld-rc.yaml .
  535  mv helloworld-rc.yaml 00-Helloworld-rc.yaml
  536  ls
  537  kubectl  apply -f 00-Helloworld-rc.yaml
  538  kubectl  delete -f 00-Helloworld-rc.yaml
  539  ls
  540  cat 01-helloworld.yaml
  541  kubectl  apply -f 01-helloworld.yaml
  542  kubectl  get nodes --show-labels
  543  kubectl  apply -f 00-Helloworld-rc.yaml
  544  kubectl  delete -f 00-Helloworld-rc.yaml
  545  kubectl  delete -f 01-helloworld.yaml
  546  kubectl  taint node worker2 app=myapp:NoSchedule
  547  kubectl  apply -f 00-Helloworld-rc.yaml
  548  kubectl  apply -f 01-helloworld.yaml
  549  ls
  550  cp -rf 01-helloworld.yaml 02-helloworld-toleration.yaml
  551  ls
  552  vim 02-helloworld-toleration.yaml
  553  ls
  554  kubectl  apply -f 02-helloworld-toleration.yaml
  555  kubectl  describe pod helloworld-2-deployment-5b54fc64d6-47sdf
  556  ls
  557  cd ..
  558  ls
  559  kubectl  delete -f 14-Affinity-with-Taint-n-Tolerations/
  560  ls
  561  git add . ; git commit -m "14-Affinity-with-Taint-n-Tolerations" ; git push
```
