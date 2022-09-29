   
    7  cat busybox.yaml 
    8  s
    9  ls
   10  kubectl  apply -f busybox.yaml 
   11  kubectl  get pods 
   12  kubectl  delete -f ../07-Service/
   13  kubectl  get pods 
   14  kubectl  exec -it busybox -- /bin/sh 
   15  kubectl  exec -it busybox -- cat /etc/resolv.conf 
   16  kubectl  get svc -n kube-system 
   17  kubectl  get pods  -n kube-system 
   18  ls
   19  kubectl  get pods 
   20  cat busybox.yaml 
   21  kubectl edit pod busybox 
   22  kubectl  get svc 
   23  kubectl  get pods 
   24  kubectl  expose pod my-k10s-worker2 --type=NodePort
   25  kubectl  get svc 
   26  kubectl  apply -f ../07-Service/03-app-svc-deployment.yaml 
   27  kubectl  get svc 
   28  kubectl  exec -it busybox -- cat /etc/resolv.conf 
   29  kubectl  exec -it busybox -- nslookup kubernetes
   30  kubectl  exec -it busybox -- nslookup my-k10s-worker2
   31  kubectl  exec -it busybox -- nslookup python-webapp-svc
   32  kubectl  exec -it busybox -- wget python-webapp-svc:31007/info.html
   33  kubectl  exec -it busybox -- curl python-webapp-svc:31007/info.html
   34  kubectl  exec -it busybox -- wget python-webapp-svc:31007/info
   35  ls
   36  kubectl  exec -it busybox -- cat info
   37  kubectl  get svc 
   38  kubectl  edit svc python-webapp-svc
   39  kubectl  get svc 
   40  kubectl  exec -it busybox -- rm info
   41  kubectl  exec -it busybox -- wget python-webapp-svc:31007/info
   42  kubectl  exec -it busybox -- wget python-webapp-svc:80/info
   43  kubectl  exec -it busybox -- cat info
   44  kubectl  exec -it busybox -- rm info
   45  kubectl  exec -it busybox -- wget python-webapp-svc/info
   46  ls
   48  l
   49  ls
   50  vim custom-dns.yaml 
   51  kubectl  apply -f custom-dns.yaml 
   52  kubectl  get pods 
   53  kubectl  exec -it custom-dns-example -- cat /etc/resolv.conf 
   54  ls
   55  kubectl  get svc 
   56  ls
   57  mv busybox.yaml 01-busybox.yaml 
   58  mv custom-dns.yaml 02-custom-dns.yaml
   60  ls
   61  mv busybox-headless.yaml 03-busybox-headless.yaml 
   62  ls
   63  vim 03-busybox-headless.yaml 
   64  kubectl  apply -f 03-busybox-headless.yaml 
   65  kubectl  get svc 
   66  kubectl  get pods -o wide 
   67  kubectl  exec -it busybox -- nslookup python-webapp-svc
   68  kubectl  exec -it busybox -- nslookup default-subdomain
   69  kubectl  exec -it busybox -- nslookup busybox-1.default-subdomain
   70  kubectl  exec -it busybox -- nslookup busybox-2.default-subdomain
   71  ls
   72  history 
   73  history > README.md 
