# p-14653-1-mission
- 0008 완료

---

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl set image deployment/nginx-deployment nginx=nginx:1.26
deployment.apps/nginx-deployment image updated

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl rollout status deployment/nginx-deployment
Waiting for deployment "nginx-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "nginx-deployment" rollout to finish: 1 old replicas are pending termination...
deployment "nginx-deployment" successfully rolled out

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get rs
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-54c468ccc7   3         3         3       23s
nginx-deployment-7c9dddfb48   0         0         0       8m3s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl rollout history deployment/nginx-deployment
deployment.apps/nginx-deployment
REVISION  CHANGE-CAUSE
1         <none>
2         <none>


early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl annotate deployment/nginx-deployment kubernetes.io/change-cause="Update to nginx 1.26"
deployment.apps/nginx-deployment annotated

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl rollout undo deployment/nginx-deployment
deployment.apps/nginx-deployment rolled back

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl annotate deployment/nginx-deployment kubernetes.io/change-cause="Update to nginx 1.26"
deployment.apps/nginx-deployment annotated

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl rollout undo deployment/nginx-deployment --to-revision=1
error: unable to find specified revision 1 in history

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl describe deployment nginx-deployment
Name:                   nginx-deployment
Namespace:              default
CreationTimestamp:      Wed, 31 Dec 2025 16:33:44 +0900
Labels:                 app=nginx
Annotations:            deployment.kubernetes.io/revision: 3
                        kubernetes.io/change-cause: Update to nginx 1.26
Selector:               app=nginx
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:      nginx:1.25
    Port:       80/TCP
    Host Port:  0/TCP
    Limits:
      cpu:     200m
      memory:  128Mi
    Requests:
      cpu:         100m
      memory:      64Mi
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  nginx-deployment-54c468ccc7 (0/0 replicas created)
NewReplicaSet:   nginx-deployment-7c9dddfb48 (3/3 replicas created)
Events:
  Type    Reason             Age                  From                   Message
  ----    ------             ----                 ----                   -------
  Normal  ScalingReplicaSet  9m7s                 deployment-controller  Scaled up replica set nginx-deployment-7c9dddfb48 from 0 to 3
  Normal  ScalingReplicaSet  8m54s                deployment-controller  Scaled up replica set nginx-deployment-7c9dddfb48 from 3 to 5
  Normal  ScalingReplicaSet  8m21s                deployment-controller  Scaled down replica set nginx-deployment-7c9dddfb48 from 5 to 2
  Normal  ScalingReplicaSet  87s                  deployment-controller  Scaled up replica set nginx-deployment-54c468ccc7 from 0 to 1
  Normal  ScalingReplicaSet  78s                  deployment-controller  Scaled down replica set nginx-deployment-7c9dddfb48 from 3 to 2
  Normal  ScalingReplicaSet  78s                  deployment-controller  Scaled up replica set nginx-deployment-54c468ccc7 from 1 to 2
  Normal  ScalingReplicaSet  77s                  deployment-controller  Scaled down replica set nginx-deployment-7c9dddfb48 from 2 to 1
  Normal  ScalingReplicaSet  77s                  deployment-controller  Scaled up replica set nginx-deployment-54c468ccc7 from 2 to 3
  Normal  ScalingReplicaSet  20s (x2 over 5m22s)  deployment-controller  Scaled up replica set nginx-deployment-7c9dddfb48 from 2 to 3
  Normal  ScalingReplicaSet  19s (x6 over 75s)    deployment-controller  (combined from similar events): Scaled down replica set nginx-deployment-54c468ccc7 from 1 to 0

early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-deployment.yaml

<img width="1512" height="1316" alt="image" src="https://github.com/user-attachments/assets/feb0a575-0f12-4e91-9e68-b7e5a60b5c05" />



