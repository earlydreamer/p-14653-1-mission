# p-14653-1-mission
- 0003 완료

  
early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl run nginx-pod --image=nginx:latest
pod/nginx-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          11s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -w
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          16s


early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl describe pod nginx-pod
Name:             nginx-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             docker-desktop/192.168.65.3
Start Time:       Wed, 31 Dec 2025 15:33:33 +0900
Labels:           run=nginx-pod
Annotations:      <none>
Status:           Running
IP:               10.1.0.14
IPs:
  IP:  10.1.0.14
Containers:
  nginx-pod:
    Container ID:   docker://834fd264e0b2e85d4a405c7e4505c374fa39d262eed785952bb8a84839f3ac4c
    Image:          nginx:latest
    Image ID:       docker-pullable://nginx@sha256:ca871a86d45a3ec6864dc45f014b11fe626145569ef0e74deaffc95a3b15b430
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 31 Dec 2025 15:33:42 +0900
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mgdzp (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-mgdzp:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  27s   default-scheduler  Successfully assigned default/nginx-pod to docker-desktop
  Normal  Pulling    27s   kubelet            Pulling image "nginx:latest"
  Normal  Pulled     19s   kubelet            Successfully pulled image "nginx:latest" in 7.587s (7.587s including waiting). Image size: 59797235 bytes.
  Normal  Created    19s   kubelet            Created container: nginx-pod
  Normal  Started    19s   kubelet            Started container nginx-pod

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec -it nginx-pod -- bash
root@nginx-pod:/# cat /etc/nginx/nginx.conf

user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
root@nginx-pod:/# exit
exit

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl logs nginx-pod
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2025/12/31 06:33:42 [notice] 1#1: using the "epoll" event method
2025/12/31 06:33:42 [notice] 1#1: nginx/1.29.4
2025/12/31 06:33:42 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19)
2025/12/31 06:33:42 [notice] 1#1: OS: Linux 6.6.87.2-microsoft-standard-WSL2
2025/12/31 06:33:42 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2025/12/31 06:33:42 [notice] 1#1: start worker processes
2025/12/31 06:33:42 [notice] 1#1: start worker process 29
2025/12/31 06:33:42 [notice] 1#1: start worker process 30
2025/12/31 06:33:42 [emerg] 29#29: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 31
2025/12/31 06:33:42 [emerg] 30#30: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [emerg] 31#31: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 32
2025/12/31 06:33:42 [notice] 1#1: start worker process 33
2025/12/31 06:33:42 [emerg] 32#32: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [emerg] 33#33: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 34
2025/12/31 06:33:42 [emerg] 34#34: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 35
2025/12/31 06:33:42 [emerg] 35#35: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 36
2025/12/31 06:33:42 [emerg] 36#36: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 37
2025/12/31 06:33:42 [emerg] 37#37: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 38
2025/12/31 06:33:42 [emerg] 38#38: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 39
2025/12/31 06:33:42 [emerg] 39#39: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 40
2025/12/31 06:33:42 [notice] 1#1: start worker process 41
2025/12/31 06:33:42 [emerg] 40#40: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [emerg] 41#41: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 42
2025/12/31 06:33:42 [notice] 1#1: start worker process 43
2025/12/31 06:33:42 [emerg] 42#42: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [emerg] 43#43: io_setup() failed (11: Resource temporarily unavailable)
2025/12/31 06:33:42 [notice] 1#1: start worker process 44
2025/12/31 06:33:42 [emerg] 44#44: io_setup() failed (11: Resource temporarily unavailable)

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod nginx-pod
pod "nginx-pod" deleted from default namespace



  
