# p-14653-1-mission
- 0006 완료

---
<img width="1501" height="1149" alt="image" src="https://github.com/user-attachments/assets/f7ef849d-0d2a-494d-884b-57db59881e2b" />

early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-deployment.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-52b2n   1/1     Running   0          11s
nginx-deployment-7c9dddfb48-csvtl   1/1     Running   0          11s
nginx-deployment-7c9dddfb48-j84xh   1/1     Running   0          11s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod nginx-deployment-7c9dddfb48-j84xh
pod "nginx-deployment-7c9dddfb48-j84xh" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-7c9dddfb48-52b2n   1/1     Running   0          44s
nginx-deployment-7c9dddfb48-csvtl   1/1     Running   0          44s
nginx-deployment-7c9dddfb48-ztj7d   1/1     Running   0          6s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete -f nginx-deployment.yaml
deployment.apps "nginx-deployment" deleted from default namespace
