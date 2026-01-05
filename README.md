# p-14653-1-mission
- 0012 완료



---
early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod app-pod
pod "app-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete configmap app-config
configmap "app-config" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ vi app-configmap.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl create configmap app-config \
  --from-literal=APP_ENV=development \
  --from-literal=APP_DEBUG=true
configmap/app-config created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete configmap app-config
configmap "app-config" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pod-with-configmap.yaml
pod/app-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f app-configmap.yaml
configmap/app-config created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pod-with-configmap.yaml
pod/app-pod unchanged

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec app-pod -- env | grep APP
APP_ENV=development
APP_DEBUG=true

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec -it app-pod -- bash
root@app-pod:/# development
bash: development: command not found
root@app-pod:/# echo $APP_ENV
development
root@app-pod:/# echo $DATABASE_HOST
db-service
root@app-pod:/# exit
exit

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec app-pod -- env | grep APP
APP_ENV=development
APP_DEBUG=true

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get configmap app-config -o yaml
apiVersion: v1
data:
  APP_DEBUG: "true"
  APP_ENV: development
  DATABASE_HOST: db-service
  DATABASE_PORT: "5432"
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"APP_DEBUG":"true","APP_ENV":"development","DATABASE_HOST":"db-service","DATABASE_PORT":"5432"},"kind":"ConfigMap","metadata":{"annotations":{},"name":"app-config","namespace":"default"}}
  creationTimestamp: "2026-01-05T03:02:27Z"
  name: app-config
  namespace: default
  resourceVersion: "654435"
  uid: deba1176-8ea7-4090-aefd-65930e0789bb

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl edit configmap app-config
Edit cancelled, no changes made.

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod app-pod
pod "app-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete configmap app-config
configmap "app-config" deleted from default namespace
