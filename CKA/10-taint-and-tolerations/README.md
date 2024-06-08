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

## Display available taints of a node
```
controlplane $ kubectl get nodes node01  -o jsonpath='{.spec.taints}' | jq
[
  {
    "effect": "NoSchedule",
    "key": "kubernetes.io/disk",
    "value": "ssd"
  }
]
```

## Display tolerations of pod
```
controlplane $ kubectl get pods  -o jsonpath='{.items[*].spec.tolerations}' | jq 
[
  {
    "effect": "NoSchedule",
    "key": "kubernetes.io/disk",
    "operator": "Equal",
    "value": "ssd"
  },
  {
    "effect": "NoExecute",
    "key": "node.kubernetes.io/not-ready",
    "operator": "Exists",
    "tolerationSeconds": 300
  },
  {
    "effect": "NoExecute",
    "key": "node.kubernetes.io/unreachable",
    "operator": "Exists",
    "tolerationSeconds": 300
  }
]
[
  {
    "effect": "NoSchedule",
    "key": "kubernetes.io/disk",
    "operator": "Equal",
    "value": "hdd"
  },
  {
    "effect": "NoExecute",
    "key": "node.kubernetes.io/not-ready",
    "operator": "Exists",
    "tolerationSeconds": 300
  },
  {
    "effect": "NoExecute",
    "key": "node.kubernetes.io/unreachable",
    "operator": "Exists",
    "tolerationSeconds": 300
  }
]
controlplane $
```