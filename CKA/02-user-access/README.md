# 02. Grant user access to kubernetes cluster

This documentation provides commands to grant acces to an user to kubernetes cluster.

## Create SSL private key
```
controlplane $ openssl genrsa -out example-user.key 2048
Generating RSA private key, 2048 bit long modulus (2 primes)
...........................................................+++++
.........................................................................................................................................................+++++
e is 65537 (0x010001)
controlplane $
```

## Create CSR
```
controlplane $ openssl req -new -key example-user.key -out example-user.csr -subj "/CN=example-user"
controlplane $
```

## Create kubernetes certificate siging request object
```
controlplane $ cat example-user.csr | base64 | tr -d "\n"
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1hEQ0NBVVFDQVFBd0Z6RVZNQk1HQTFVRUF3d01aWGhoYlhCc1pTMTFjMlZ5TUlJQklqQU5CZ2txaGtpRwo5dzBCQVFFRkFBT0NBUThBTUlJQkNnS0NBUUVBMXg3YWQvS0VEQitrajlBdlhTdDFKNCt3RW9BWnRUeUUxaUJYCjRkMGtGcThORk9NQTFyVGVWb3lPelFNM0t4ZGVIRkdwc0RDb2lPalRLaVBYWlR2a0NxTHlTY0JNclFGODI4ZU0KYkxWRVJOeWU0RW80clJtNmgwUzZob2lmTU9pOFBxYnBTKytMdkZwY1dqMnB2S3VObGZqVnAvb0RMRFJaZlFrNQpRTlh1V0o2OTFDQWtpclZWTjhwcEwxQ2FhdkdEbDVVZEVic3BvVTc1bHVWWDJCem1TOGJwVkgvNmROd3BJd21MCm91dmRCUmhWNnFxVEttMjhBU1h4czBRSkdkS2hNUWt6YU4weWg3M3Z2ZjNNMm5CYkZidFJtZUplYzY1ejV3eUcKTXk5ekF5N0ZxWGRqdjNHL204bDBnZmxHaE5SdkhmUEFVSDRuRVFIUzNLeGRSbXpjQ1FJREFRQUJvQUF3RFFZSgpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBY3F6NG51T2hTcDN1c09SdHB4RkJxYXY5aWFENEJpTm1sb0YxdzJkUGJ5CkVSbUQxaVgrRE5ZVUYwWjhwUVhMYzBHdGtiNUR5MElpS1VDaUxGN1RkQmdwOFNERllCMjVTanVkT2VheWxDcVcKREVxaXpHVytMWk9RVDZuRjM0bnNWWXEvVWxDbWRTenc1R05keElGSXVRTUV1ejNMQjJ6SkVBYmFNT3FNdFhrTwpaQm5RTnBYelczZjVhdHpFdmdhRS9ZRFNyejk4enpKR2NINkhpU0ZaZFRpTUVZNHNtMU1aekJKakxDN3BVNE9GClBkUkd3K2MxWVpkTFpPQUFQT21zQ0NhOXJseU14SHJqWnJ1a1NZQTRXNk9PWU1FRWYzSW9tcG1XdHA2UUJFT04KT3M0Q1dWV3laUDNhck9uRlRxMVo4T2ZoM2M4MjE0Tlk5TWE5anlyWE9IWT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUgUkVRVUVTVC0tLS0tCg== 
controlplane $ 
controlplane $ vim cert-req.yaml
controlplane $ kubectl apply -f cert-req.yaml 
certificatesigningrequest.certificates.k8s.io/example-user created
controlplane $
```

## Approved the certificate signing request
```
controlplane $ kubectl get csr 
NAME           AGE   SIGNERNAME                                    REQUESTOR                  REQUESTEDDURATION   CONDITION
csr-c2r9x      21d   kubernetes.io/kube-apiserver-client-kubelet   system:bootstrap:i7jvby    <none>              Approved,Issued
csr-w8xvk      21d   kubernetes.io/kube-apiserver-client-kubelet   system:node:controlplane   <none>              Approved,Issued
example-user   88s   kubernetes.io/kube-apiserver-client           kubernetes-admin           24h                 Pending
controlplane $ kubectl certificate approve example-user 
certificatesigningrequest.certificates.k8s.io/example-user approved
controlplane $ 
```

## Extract certificate from the certificate signing request
```
controlplane $ kubectl get csr example-user -o jsonpath='{.status.certificate}'| base64 -d > example-user.crt
controlplane $ 
```

## Create a developer role
```
controlplane $ kubectl create role developer --verb=get,list,create,delete --resource=pods
role.rbac.authorization.k8s.io/developer created
controlplane $ 
```

## Create rolebinding for the user
```
controlplane $ kubectl create rolebinding developer-binding-example-user --role=developer --user=example-user  
rolebinding.rbac.authorization.k8s.io/developer-binding-example-user created
controlplane $
```

## Add the user into kubeconfig file
```
controlplane $ kubectl config set-credentials example-user --client-key=example-user.key  --client-certificate=example-user.crt --embed-certs=true
User "example-user" set.
controlplane $
```

## Add the context
```
controlplane $ kubectl config set-context example-user --cluster=kubernetes --user=example-user 
Context "example-user" created.
controlplane $
```

## Use the newly created context
```
controlplane $ kubectl config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
          example-user                  kubernetes   example-user       
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   
controlplane $ kubectl config use-context example-user
Switched to context "example-user".
controlplane $ 
```

## Check the permission for the user `example-user`
```
controlplane $ kubectl auth can-i create pods                  
yes
controlplane $ kubectl auth can-i create deployments
no
controlplane $
```