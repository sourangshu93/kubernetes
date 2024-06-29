# 06. StatefulSets

## Get the statefulset
```
controlplane $ kubectl get statefulsets.apps 
NAME   READY   AGE
web    3/3     2m12s
controlplane $
```

## Get the running pods
```
controlplane $ kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
web-0   1/1     Running   0          112s
web-1   1/1     Running   0          99s
web-2   1/1     Running   0          87s
controlplane $
```