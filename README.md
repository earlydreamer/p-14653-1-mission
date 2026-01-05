# p-14653-1-mission
- 0009 완료

---

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-deployment.yaml
Error from server (BadRequest): error when creating "nginx-deployment.yaml": Deployment in version "v1" cannot be handled as a Deployment: strict decoding error: unknown field "spec.template.spec.rollingUpdate", unknown field "spec.template.spec.type"

early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-deployment.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ rm nginx-deployment.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-deployment.yaml

[No write since last change]

Press ENTER or type command to continue

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-service-clusterip.yaml:

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-2tf5k   1/1     Running   0          106s
nginx-deployment-7c9dddfb48-rwj64   1/1     Running   0          106s
nginx-deployment-7c9dddfb48-zfvnq   1/1     Running   0          106s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-service-clusterip.yaml
service/nginx-service unchanged

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get services
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP   5d17h
nginx-service   ClusterIP   10.102.131.68   <none>        80/TCP    9m42s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl describe service nginx-service
Name:                     nginx-service
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=nginx
Type:                     ClusterIP
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.102.131.68
IPs:                      10.102.131.68
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
Endpoints:                10.1.0.47:80,10.1.0.46:80,10.1.0.48:80
Session Affinity:         None
Internal Traffic Policy:  Cluster
Events:                   <none>

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl run curl-test --image=curlimages/curl -it --rm --restart=Never -- curl nginx-service
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
pod "curl-test" deleted from default namespace
