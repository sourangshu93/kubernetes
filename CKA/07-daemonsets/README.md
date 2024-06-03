# 07. DaemonSet


## Show the DaemonSets and display the pods
```
controlplane $ kubectl get daemonsets.apps --namespace production 
NAME         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
example-ds   2         2         0       2            0           <none>          9s
controlplane $ kubectl get pods --namespace production -o wide
NAME               READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
example-ds-4587x   1/1     Running   0          70s   192.168.0.4   controlplane   <none>           <none>
example-ds-bbx95   1/1     Running   0          70s   192.168.1.4   node01         <none>           <none>
controlplane $ 
```
