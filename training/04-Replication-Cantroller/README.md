```
  mkdir 04-Replication-Cantroller
  cd 04-Replication-Cantroller/
  vim helloworld-rc.yaml
  kubectl apply -f helloworld-rc.yaml
  cat helloworld-rc.yaml
  kubectl get rc
  kubectl describe rc helloworld-controller
  kubectl delete pod helloworld-controller-x569j helloworld-controller-d8mjc
  kubectl describe rc helloworld-controller
  kubectl get rc
  kubectl scale replicas=1 rc helloworld-controller
  kubectl scale --replicas=1 rc helloworld-controller
  kubectl get rc
  kubectl delete pod helloworld-controller-n9n8k
  kubectl scale --replicas=5 rc helloworld-controller
  kubectl delete pod hello-k8s-2
  cat helloworld-rc.yaml
  kubectl apply -f helloworld-rc.yaml
  kubectl delete -f helloworld-rc.yaml

```

```
 watch -n .5 kubectl get pods -o wide
```


Note Point : In Case you are getting imagepull error stating that you have reached to max limit of downloads, then apply the following solution. 

# Docker login
```
docker login
ls /root/.docker/config.json
```

# Create a Secret in K8s for Docker Registry
```
kubectl create secret generic regcred --from-file=.dockerconfigjson=/root/.docker/config.json --type=kubernetes.io/dockerconfigjson

kubectl get secrets
```

## Update the Pull Defination in Yaml File 
```
      imagePullSecrets:
      - name: regcred
```

## Now deploy helloworld Repication Cantroller:
```
kubectl apply -f helloworld-rc.yaml
```