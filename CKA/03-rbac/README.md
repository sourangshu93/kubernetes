# O3. Role Based Access Control (RBAC)

This documentation provides imperative commands to manage kubernetes RBAC.

## Create Service Account
```
controlplane $ kubectl create serviceaccount example-sa -n production
serviceaccount/example-sa created
controlplane $
```

## Create ClusterRole
```
controlplane $ kubectl create clusterrole example-clusterrole --resource=pods --resource=deployments,statefulsets --verb=create,list,get  --resource=statefulsets --verb=create,list,get           
clusterrole.rbac.authorization.k8s.io/example-clusterrole created
controlplane $
```

## Create ClusterRoleBinding
```
controlplane $ kubectl create clusterrolebinding example-clusterrole-sa-binding --clusterrole=example-clusterrole --serviceaccount=production:example-sa                       
clusterrolebinding.rbac.authorization.k8s.io/example-clusterrole-sa-binding created
controlplane $
```
## Craete Role
```
controlplane $ kubectl create role -n production example-role --resource=pods --verb=get,list,patch,create,delete,watch --resource=deployments,statefulsets --verb=get,list,patch,create,delete,watch
role.rbac.authorization.k8s.io/example-role created
controlplane $
```
## Create RoleBinding
```
controlplane $ kubectl create rolebinding example-role-sa-binding -n production --serviceaccount=production:example-sa --role=example-role
rolebinding.rbac.authorization.k8s.io/example-role-sa-binding created
controlplane $
```

## Validating ServiceAccount permissions

```
# Checking if serviceaccount has permission to create deployment
controlplane $ kubectl auth can-i create deployment -n production --as system:serviceaccount:production:example-sa
yes
controlplane $
# Checking if serviceaccount has permission to create daemonset
controlplane $ kubectl auth can-i create daemonset -n production --as system:serviceaccount:production:example-sa
no
controlplane $
```
