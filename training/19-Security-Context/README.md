```
 1006  kubectl  apply -f 01-Pod-1.yaml
 1007  kubectl  get pods
 1008  kubectl  exec -it pod-1 -- bash
 1009  kubectl  exec -it pod-1 -- sh
 1010  ls
 1011  vim 02-Pod-Context.yaml
 1012  kubectl  apply -f 02-Pod-Context.yaml
 1013  vim 02-Pod-Context.yaml
 1014  kubectl  apply -f 02-Pod-Context.yaml
 1015  kubectl  get pods
 1016  kubectl  exec -it pod-context -- sh
 1017  ls
 1018  vim 03-Pod-FS-Context.yaml
 1019  kubectl  apply -f 03-Pod-FS-Context.yaml
 1020  kubectl  get pods
 1021  kubectl  exec -it security-context-demo -- sh
```
