# 01. Setting up a kubernetes cluster

## Cluster details
- Use Kubernetes version v1.30.0
- Use a Pod-Network-Cidr of 192.168.0.0/16
- Ignore preflight errors for NumCPU and Mem
- Copy the default kubectl admin.conf to /root/.kube/config

## Use kubeadm to initialize the cluster with mentioned details
```
controlplane $ kubeadm init --kubernetes-version=1.30.0 --pod-network-cidr 192.168.0.0/16  --ignore-preflight-errors=NumCPU --ignore-preflight-errors=Mem
[init] Using Kubernetes version: v1.30.0
[preflight] Running pre-flight checks
        [WARNING NumCPU]: the number of available CPUs 1 is less than the required 2
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
W0629 07:11:42.559302    6319 checks.go:844] detected that the sandbox image "registry.k8s.io/pause:3.5" of the container runtime is inconsistent with that used by kubeadm.It is recommended to use "registry.k8s.io/pause:3.9" as the CRI sandbox image.
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [controlplane kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 172.30.1.2]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [controlplane localhost] and IPs [172.30.1.2 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [controlplane localhost] and IPs [172.30.1.2 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "super-admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
[control-plane] Creating static Pod manifest for "kube-scheduler"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests"
[kubelet-check] Waiting for a healthy kubelet. This can take up to 4m0s
[kubelet-check] The kubelet is healthy after 503.037712ms
[api-check] Waiting for a healthy API server. This can take up to 4m0s
[api-check] The API server is healthy after 9.501805591s
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node controlplane as control-plane by adding the labels: [node-role.kubernetes.io/control-plane node.kubernetes.io/exclude-from-external-load-balancers]
[mark-control-plane] Marking the node controlplane as control-plane by adding the taints [node-role.kubernetes.io/control-plane:NoSchedule]
[bootstrap-token] Using token: 3q2e73.qr58qxxaci2romst
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] Configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] Configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.30.1.2:6443 --token 3q2e73.qr58qxxaci2romst \
        --discovery-token-ca-cert-hash sha256:763ee5cfc8e6635004d8410d2f1a257c17ce555e9b5da797d9921b66b9ac6fe4 
controlplane $
```

## Copy the admin configuration to .kube directory
```
controlplane $ cp /etc/kubernetes/admin.conf /root/.kube/config
controlplane $ sudo chown $(id -u):$(id -g) /root/.kube/config
controlplane $ kubectl get pods -A
NAMESPACE     NAME                                   READY   STATUS              RESTARTS   AGE
kube-system   coredns-7db6d8ff4d-77l2c               0/1     ContainerCreating   0          112s
kube-system   coredns-7db6d8ff4d-rvzj5               0/1     ContainerCreating   0          112s
kube-system   etcd-controlplane                      1/1     Running             0          2m6s
kube-system   kube-apiserver-controlplane            1/1     Running             0          2m5s
kube-system   kube-controller-manager-controlplane   1/1     Running             0          2m8s
kube-system   kube-proxy-94bql                       1/1     Running             0          112s
kube-system   kube-scheduler-controlplane            1/1     Running             0          2m6s
controlplane $ 
```

## Check number of nodes
```
controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE     VERSION
controlplane   Ready    control-plane   4m55s   v1.30.0
controlplane $
```

## Create node join command
```
controlplane $ kubeadm token create --print-join-command
kubeadm join 172.30.1.2:6443 --token 3p82zw.015rwi3mcze83rpc --discovery-token-ca-cert-hash sha256:763ee5cfc8e6635004d8410d2f1a257c17ce555e9b5da797d9921b66b9ac6fe4 
controlplane $
```

## Join the worker node to cluster
```
controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
node-summer $ kubeadm join 172.30.1.2:6443 --token 3p82zw.015rwi3mcze83rpc --discovery-token-ca-cert-hash sha256:763ee5cfc8e6635004d8410d2f1a257c17ce555e9b5da797d9921b66b9ac6fe4
[preflight] Running pre-flight checks
        [WARNING Hostname]: hostname "node-summer" could not be reached
        [WARNING Hostname]: hostname "node-summer": lookup node-summer on 8.8.8.8:53: no such host
[preflight] Reading configuration from the cluster...
[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -o yaml'
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Starting the kubelet
[kubelet-check] Waiting for a healthy kubelet. This can take up to 4m0s
[kubelet-check] The kubelet is healthy after 1.004687031s
[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.

node-summer $ 
```

##  Check if the worker node has joined the cluster
```
controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE     VERSION
controlplane   Ready    control-plane   9m38s   v1.30.0
node-summer    Ready    <none>          115s    v1.30.0
controlplane $
```