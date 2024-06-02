# 04. Pods

This documentation provides imperative commands to create and manage pods in kubernetes.

# Create pod using command line
```
controlplane $ kubectl run example-pod --image=nginx
pod/example-pod created
controlplane $ kubectl get pods                     
NAME          READY   STATUS    RESTARTS   AGE
example-pod   1/1     Running   0          9s
controlplane $ 
```

## Init containers
```
controlplane $ kubectl get pods
NAME               READY   STATUS     RESTARTS   AGE
example-init-pod   0/1     Init:0/1   0          27s
controlplane $ kubectl get pods
NAME               READY   STATUS            RESTARTS   AGE
example-init-pod   0/1     PodInitializing   0          68s
controlplane $ kubectl get pods
NAME               READY   STATUS    RESTARTS   AGE
example-init-pod   1/1     Running   0          71s
controlplane $ 
```


