# 05. Deployment

## Create ReplicationController
```
controlplane $ kubectl get replicationcontrollers 
NAME         DESIRED   CURRENT   READY   AGE
example-rc   2         2         2       10s
controlplane $ kubectl get pods                   
NAME               READY   STATUS    RESTARTS   AGE
example-rc-kqxd7   1/1     Running   0          22s
example-rc-n5d5n   1/1     Running   0          22s
controlplane $
```

## Create ReplicaSet
```
controlplane $ kubectl get replicasets.apps --namespace=production
NAME         DESIRED   CURRENT   READY   AGE
example-rs   2         2         2       24s
controlplane $ kubectl get pods --namespace=production
NAME               READY   STATUS    RESTARTS   AGE
example-rs-ffc9d   1/1     Running   0          31s
example-rs-pf8jm   1/1     Running   0          31s
controlplane $ 
```

## Create Deployment
```
controlplane $ kubectl create deployment example-app --image=nginx --replicas=2 --namespace=production
deployment.apps/example-app created
controlplane $ kubectl get deployments.apps --namespace=production 
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
example-app   2/2     2            2           45s
controlplane $ kubectl get pods --namespace=production 
NAME                          READY   STATUS    RESTARTS   AGE
example-app-dc5768494-czrcj   1/1     Running   0          64s
example-app-dc5768494-kvhw2   1/1     Running   0          64s
controlplane $ 
```
# Scale up/down Deployment
```
controlplane $ kubectl scale deployment --namespace=production example-app --replicas=3
deployment.apps/example-app scaled
controlplane $ kubectl get deployments.apps --namespace=production 
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
example-app   3/3     3            3           2m41s
controlplane $ kubectl get pods --namespace=production 
NAME                          READY   STATUS    RESTARTS   AGE
example-app-dc5768494-czrcj   1/1     Running   0          2m46s
example-app-dc5768494-kvhw2   1/1     Running   0          2m46s
example-app-dc5768494-m2n2v   1/1     Running   0          17s
controlplane $ 
```

## Update image of a deployment
```
controlplane $ kubectl get pods --namespace=production -o wide
NAME                         READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
example-app-99dd6d5b-vz5nz   1/1     Running   0          28s   192.168.0.8   controlplane   <none>           <none>
example-app-99dd6d5b-w6fv2   1/1     Running   0          28s   192.168.1.9   node01         <none>           <none>
controlplane $ kubectl get deployments.apps --namespace=production -o wide
NAME          READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
example-app   2/2     2            2           40s   nginx        nginx:1.14.2   app=example-app          
controlplane $ kubectl set image --namespace=production deployment example-app nginx=nginx:1.16.1
deployment.apps/example-app image updated
controlplane $ kubectl get deployments.apps --namespace=production -o wide
NAME          READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
example-app   2/2     1            2           2m24s   nginx        nginx:1.16.1   app=example-app
controlplane $ kubectl rollout status deployment --namespace=production example-app 
deployment "example-app" successfully rolled out
controlplane $
controlplane $ kubectl get replicasets.apps --namespace=production 
NAME                     DESIRED   CURRENT   READY   AGE
example-app-545cf4d579   2         2         2       3m16s
example-app-99dd6d5b     0         0         0       5m32s
controlplane $ 
```

## Rollback a Deployment
```
controlplane $ kubectl get deployments.apps --namespace=production example-app -o wide
NAME          READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
example-app   2/2     2            2           9m25s   nginx        nginx:1.16.1   app=example-app
controlplane $ kubectl rollout history deployment/example-app --namespace=production 
deployment.apps/example-app 
REVISION  CHANGE-CAUSE
1         <none>
2         <none>

controlplane $ kubectl rollout undo deployment --namespace=production example-app             
deployment.apps/example-app rolled back
controlplane $ kubectl get deployments.apps --namespace=production example-app -o wide
NAME          READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
example-app   2/2     2            2           12m   nginx        nginx:1.14.2   app=example-app
controlplane $
```
