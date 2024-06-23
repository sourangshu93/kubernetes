# 14. Autoscaling

```
controlplane $ kubectl create deployment example-deployment --image=nginx --replicas=2
deployment.apps/example-deployment created
controlplane $
```

```
controlplane $ kubectl get deployments.apps 
NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
example-deployment   2/2     2            2           11s
controlplane $
```

```
controlplane $ kubectl autoscale deployment example-deployment --max 10 --min 3 --cpu-percent 75
horizontalpodautoscaler.autoscaling/example-deployment autoscaled
controlplane $
```

```
controlplane $ kubectl get hpa
NAME                 REFERENCE                       TARGETS              MINPODS   MAXPODS   REPLICAS   AGE
example-deployment   Deployment/example-deployment   cpu: <unknown>/75%   3         10        0          14s
controlplane $ 
```

```
controlplane $ kubectl get deployments.apps example-deployment 
NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
example-deployment   3/3     3            3           6m15s
controlplane $ kubectl get pods                                
NAME                                  READY   STATUS    RESTARTS   AGE
example-deployment-78d4d5dbfb-9phd4   1/1     Running   0          6m23s
example-deployment-78d4d5dbfb-n5zg9   1/1     Running   0          6m23s
example-deployment-78d4d5dbfb-xd6bg   1/1     Running   0          5m5s
controlplane $ 
```