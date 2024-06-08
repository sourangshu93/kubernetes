# 10. Taints and Tolerations

## Adding taints to kubernetes nodes
```
controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   27d   v1.30.0
node01         Ready    <none>          27d   v1.30.0
```
```
controlplane $ kubectl taint node node01 kubernetes.io/disk=ssd:NoSchedule
node/node01 tainted
controlplane $
```
