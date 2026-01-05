# p-14653-1-mission
- 0013 완료



---early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=secretpassword123
secret/db-secret created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get secret db-secret -o yaml
apiVersion: v1
data:
  password: c2VjcmV0cGFzc3dvcmQxMjM=
  username: YWRtaW4=
kind: Secret
metadata:
  creationTimestamp: "2026-01-05T03:08:25Z"
  name: db-secret
  namespace: default
  resourceVersion: "654925"
  uid: 07a3ac40-77c4-467d-a108-e1dfdb79dc71
type: Opaque

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get secret db-secret -o jsonpath='{.data.username}' | base64 -d
admin
early@JAKEPARK-MAINPC MINGW64 ~
$ echo -n "admin" | base64
YWRtaW4=

early@JAKEPARK-MAINPC MINGW64 ~
$ echo -n "secretpass123" | base64
c2VjcmV0cGFzczEyMw==

early@JAKEPARK-MAINPC MINGW64 ~
$ vi db-secret.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ vi pod-with-secret.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec -it app-pod -- bash
Error from server (NotFound): pods "app-pod" not found

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pod-with-secret.yaml
pod/db-app-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec -it db-app-pod -- bash
root@db-app-pod:/# cat /etc/secrets/username
cat: /etc/secrets/username: No such file or directory
root@db-app-pod:/# exit
exit
command terminated with exit code 127

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod db-app-pod
pod "db-app-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete secret db-secret
secret "db-secret" deleted from default namespace
$ kubectl delete configmap app-config
configmap "app-config" deleted from default namespace
