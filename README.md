# p-14653-1-mission
- 0005 완료

---
<img width="1498" height="1135" alt="image" src="https://github.com/user-attachments/assets/be247494-9725-4068-a079-e5c92efc1a93" />

early@JAKEPARK-MAINPC MINGW64 ~
$ vi multi-container-pod.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f multi-container-pod.yaml
pod/multi-container-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods
NAME                  READY   STATUS              RESTARTS   AGE
multi-container-pod   0/2     ContainerCreating   0          5s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods
NAME                  READY   STATUS    RESTARTS   AGE
multi-container-pod   2/2     Running   0          18s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl logs multi-container-pod -c log-sidecar

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl logs multi-container-pod -c main-app
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec -it multi-container-pod -c main-app -- bash
root@multi-container-pod:/# kubectl exec multi-container-pod -c main-app -- curl localhost
bash: kubectl: command not found
root@multi-container-pod:/# exit
exit
command terminated with exit code 127

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec multi-container-pod -c main-app -- curl localhost
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0<!DOCTYPE html>
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
100   615  100   615    0     0  1099k      0 --:--:-- --:--:-- --:--:--  600k

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl logs multi-container-pod -c log-sidecar
127.0.0.1 - - [31/Dec/2025:07:17:07 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/7.88.1" "-"

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete -f multi-container-pod.yaml
pod "multi-container-pod" deleted from default namespace


early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete -f multi-container-pod.yaml
pod "multi-container-pod" deleted from default namespace

