# p-14653-1-mission
- 0011 완료

---

early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-service-lb.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-service-lb.yaml
service/nginx-lb created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get service nginx-lb
NAME       TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
nginx-lb   LoadBalancer   10.97.51.126   localhost     80:32266/TCP   7s

early@JAKEPARK-MAINPC MINGW64 ~
$ curl http://localhost
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

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl describe service nginx-lb
Name:                     nginx-lb
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=nginx
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.97.51.126
IPs:                      10.97.51.126
LoadBalancer Ingress:     localhost
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  32266/TCP
Endpoints:                10.1.0.54:80,10.1.0.53:80,10.1.0.55:80
Session Affinity:         None
External Traffic Policy:  Cluster
Internal Traffic Policy:  Cluster
Events:                   <none>

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete service nginx-lb
service "nginx-lb" deleted from default namespace
