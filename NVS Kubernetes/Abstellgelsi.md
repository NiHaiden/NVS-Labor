Ab hier lokal weil Server nix gehen tun
```
PS C:\Users\nikla> kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
deployment.apps/hello-minikube created
PS C:\Users\nikla> kubectl expose deployment hello-minikube --type=NodePort --port=8080
service/hello-minikube exposed
PS C:\Users\nikla> kubectl get services hello-minikube
NAME             TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort   10.97.44.188   <none>        8080:31564/TCP   8s
PS C:\Users\nikla> minikube service hello-minikube
|-----------|----------------|-------------|----------------------------|
| NAMESPACE |      NAME      | TARGET PORT |            URL             |
|-----------|----------------|-------------|----------------------------|
| default   | hello-minikube |        8080 | http://172.24.150.97:31564 |
|-----------|----------------|-------------|----------------------------|
🎉  Opening service default/hello-minikube in default browser...
PS C:\Users\nikla> kubectl port-forward service/hello-minikube 7080:8080
Forwarding from 127.0.0.1:7080 -> 8080
Forwarding from [::1]:7080 -> 8080
Handling connection for 7080
```
Test des Echo Servers: 
![[Pasted image 20220112162912.png]]
Info des Service: 
```
PS C:\Users\nikla> kubectl get service hello-minikube
NAME             TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort   10.97.44.188   <none>        8080:31564/TCP   7m10s
```