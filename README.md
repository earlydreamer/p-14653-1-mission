# p-14653-1-mission
- 0014 완료

---
early@JAKEPARK-MAINPC MINGW64 ~
$ vi pv-local.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ pvc-local.yaml
bash: pvc-local.yaml: command not found

early@JAKEPARK-MAINPC MINGW64 ~
$ vi pvc-local.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ vi pod-with-pvc.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pv-local.yaml
persistentvolume/local-pv created

early@JAKEPARK-MAINPC MINGW64 ~
$ 

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pvc-local.yaml
persistentvolumeclaim/local-pvc created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pod-with-pvc.yaml
pod/pvc-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pv
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM               STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
local-pv   1Gi        RWO            Retain           Bound    default/local-pvc   manual         <unset>                          14s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pvc
NAME        STATUS   VOLUME     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
local-pvc   Bound    local-pv   1Gi        RWO            manual         <unset>                 17s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- sh -c "echo 'Hello K8s' > /usr/share/nginx/html/index.html"

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- cat /usr/share/nginx/html/index.html
cat: 'C:/Program Files/Git/usr/share/nginx/html/index.html': No such file or directory
command terminated with exit code 1

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- sh -c "echo 'Hello K8s' > /usr/share/nginx/html/index.html"

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- sh -c "echo 'Hello K8s' > ./index.html"

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- cat ./index.html
Hello K8s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod pvc-pod
pod "pvc-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pod-with-pvc.yaml
pod/pvc-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- cat /usr/share/nginx/html/index.html
cat: 'C:/Program Files/Git/usr/share/nginx/html/index.html': No such file or directory
command terminated with exit code 1

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl exec pvc-pod -- ./index.html
OCI runtime exec failed: exec failed: unable to start container process: exec: "./index.html": stat ./index.html: no such file or directory
command terminated with exit code 127

early@JAKEPARK-MAINPC MINGW64 ~
$ MSYS_NO_PATHCONV=1 kubectl exec pvc-pod -- cat /usr/share/nginx/html/index.html
Hello K8s

early@JAKEPARK-MAINPC MINGW64 ~
$ MSYS_NO_PATHCONV=1 kubectl exec pvc-pod -- cat /usr/share/nginx/html/index.html
Hello K8s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod pvc-pod
pod "pvc-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f pod-with-pvc.yaml
pod/pvc-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ MSYS_NO_PATHCONV=1 kubectl exec pvc-pod -- cat /usr/share/nginx/html/index.html
Hello K8s

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pod pvc-pod
pod "pvc-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pvc local-pvc
persistentvolumeclaim "local-pvc" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl delete pv local-pv
persistentvolume "local-pv" deleted

