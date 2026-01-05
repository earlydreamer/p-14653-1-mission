# p-14653-1-mission
- 0010 완료

---

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-24f7f   1/1     Running   0          9s
nginx-deployment-7c9dddfb48-462gs   1/1     Running   0          9s
nginx-deployment-7c9dddfb48-6b9tv   1/1     Running   0          9s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-service-nodeport.yaml
service/nginx-nodeport created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get service nginx-nodeport
NAME             TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
nginx-nodeport   NodePort   10.96.150.72   <none>        80:30080/TCP   7s

early@JAKEPARK-MAINPC MINGW64 ~
$ curl http://localhost:30080
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
$ kubectl delete service nginx-nodeport
service "nginx-nodeport" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$
