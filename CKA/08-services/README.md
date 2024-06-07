# 08. Service

This document describes how to create services imperatively.

## Create NodePort Service
```
controlplane $ kubectl expose deployment frontend --name=example-nodeport-service --port=80 --target-port=80 --type=NodePort   
service/example-nodeport-service exposed
controlplane $
```

## Get service details and access the resources using NodePort service
```
controlplane $ kubectl get service example-nodeport-service 
NAME                       TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
example-nodeport-service   NodePort   10.100.30.15   <none>        80:31903/TCP   2m11s
controlplane $ 
```
```
controlplane $ kubectl get nodes -o wide
NAME           STATUS   ROLES           AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
controlplane   Ready    control-plane   26d   v1.30.0   172.30.1.2    <none>        Ubuntu 20.04.5 LTS   5.4.0-131-generic   containerd://1.7.13
node01         Ready    <none>          26d   v1.30.0   172.30.2.2    <none>        Ubuntu 20.04.5 LTS   5.4.0-131-generic   containerd://1.7.13
controlplane $
controlplane $ curl -k http://172.30.1.2:31903
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
controlplane $
```

## Create ClusterIP Service
```
controlplane $ kubectl expose deployment frontend --name=example-clusterip-service --port=80 --target-port=80 --type=NodePort
service/example-clusterip-service exposed
controlplane $ 
```

## Get service details and access the Service using ClusterIP
```
controlplane $ kubectl  get service
NAME                        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
example-clusterip-service   NodePort    10.101.105.98   <none>        80:30573/TCP   11s
kubernetes                  ClusterIP   10.96.0.1       <none>        443/TCP        26d
controlplane $ curl -k 10.101.105.98:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
controlplane $
```

## Create Loadbalancer Service

```
controlplane $ kubectl expose deployment frontend --name=example-lb-service --port=80 --target-port=9001 --type=LoadBalancer
service/example-lb-service exposed
controlplane $ kubectl get service
NAME                 TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
example-lb-service   LoadBalancer   10.98.176.25   <pending>     80:32296/TCP   12s
kubernetes           ClusterIP      10.96.0.1      <none>        443/TCP        26d
controlplane $ 
```
