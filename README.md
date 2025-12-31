# p-14653-1-mission
- 0007 완료

---
early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-deployment.yaml:

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl scale deployment nginx-deployment --replicas=5
deployment.apps/nginx-deployment scaled

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx -w
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-28z8t   1/1     Running   0          6s
nginx-deployment-7c9dddfb48-8rnhn   1/1     Running   0          19s
nginx-deployment-7c9dddfb48-l8lpv   1/1     Running   0          19s
nginx-deployment-7c9dddfb48-lfmxd   1/1     Running   0          6s
nginx-deployment-7c9dddfb48-q6vdv   1/1     Running   0          19s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl scale deployment nginx-deployment --replicas=2
deployment.apps/nginx-deployment scaled

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx -w
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-8rnhn   1/1     Running   0          69s
nginx-deployment-7c9dddfb48-l8lpv   1/1     Running   0          69s

<img width="1579" height="1224" alt="image" src="https://github.com/user-attachments/assets/1a176d44-d39c-49ea-a195-04169b995ffd" />

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment configured

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl edit deployment nginx-deployment
Edit cancelled, no changes made.

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-8rnhn   1/1     Running   0          4m57s
nginx-deployment-7c9dddfb48-l8lpv   1/1     Running   0          4m57s
nginx-deployment-7c9dddfb48-wt2rt   1/1     Running   0          72s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod nginx-deployment-7c9dddfb48-l8lpv
pod "nginx-deployment-7c9dddfb48-l8lpv" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-8rnhn   1/1     Running   0          5m30s
nginx-deployment-7c9dddfb48-dbf2f   1/1     Running   0          6s
nginx-deployment-7c9dddfb48-wt2rt   1/1     Running   0          105s

early@JAKEPARK-MAINPC MINGW64 ~
