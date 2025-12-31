# p-14653-1-mission
- 0001 완료

  
early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get nodes
NAME             STATUS   ROLES           AGE   VERSION
docker-desktop   Ready    control-plane   22h   v1.34.1

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl describe node docker-desktop
Name:               docker-desktop
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=docker-desktop
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Tue, 30 Dec 2025 17:06:49 +0900
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  docker-desktop
  AcquireTime:     <unset>
  RenewTime:       Wed, 31 Dec 2025 15:28:26 +0900
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Wed, 31 Dec 2025 15:28:04 +0900   Tue, 30 Dec 2025 17:06:48 +0900   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Wed, 31 Dec 2025 15:28:04 +0900   Tue, 30 Dec 2025 17:06:48 +0900   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Wed, 31 Dec 2025 15:28:04 +0900   Tue, 30 Dec 2025 17:06:48 +0900   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Wed, 31 Dec 2025 15:28:04 +0900   Tue, 30 Dec 2025 17:06:49 +0900   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  192.168.65.3
  Hostname:    docker-desktop
Capacity:
  cpu:                16
  ephemeral-storage:  1055762868Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             32407732Ki
  pods:               110
Allocatable:
  cpu:                16
  ephemeral-storage:  972991057538
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             32305332Ki
  pods:               110
System Info:
  Machine ID:                 21b40cf0b5d64658a7f8c679481b0d1f
  System UUID:                21b40cf0b5d64658a7f8c679481b0d1f
  Boot ID:                    e26881b7-591b-4fa5-b1a7-d097fcb2b830
  Kernel Version:             6.6.87.2-microsoft-standard-WSL2
  OS Image:                   Docker Desktop
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  docker://29.1.3
  Kubelet Version:            v1.34.1
  Kube-Proxy Version:
Non-terminated Pods:          (9 in total)
  Namespace                   Name                                      CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age 
  ---------                   ----                                      ------------  ----------  ---------------  -------------  --- 
  kube-system                 coredns-66bc5c9577-f4f4z                  100m (0%)     0 (0%)      70Mi (0%)        170Mi (0%)     22h 
  kube-system                 coredns-66bc5c9577-mvtr4                  100m (0%)     0 (0%)      70Mi (0%)        170Mi (0%)     22h 
  kube-system                 etcd-docker-desktop                       100m (0%)     0 (0%)      100Mi (0%)       0 (0%)         22h 
  kube-system                 kube-apiserver-docker-desktop             250m (1%)     0 (0%)      0 (0%)           0 (0%)         22h 
  kube-system                 kube-controller-manager-docker-desktop    200m (1%)     0 (0%)      0 (0%)           0 (0%)         22h 
  kube-system                 kube-proxy-jvffh                          0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h 
  kube-system                 kube-scheduler-docker-desktop             100m (0%)     0 (0%)      0 (0%)           0 (0%)         22h 
  kube-system                 storage-provisioner                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h 
  kube-system                 vpnkit-controller                         0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h 
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                850m (5%)   0 (0%)
  memory             240Mi (0%)  340Mi (1%)
  ephemeral-storage  0 (0%)      0 (0%)
  hugepages-1Gi      0 (0%)      0 (0%)
  hugepages-2Mi      0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                From             Message
  ----    ------                   ----               ----             -------
  Normal  Starting                 37m                kube-proxy
  Normal  Starting                 37m                kubelet          Starting kubelet.
  Normal  NodeHasSufficientMemory  37m (x8 over 37m)  kubelet          Node docker-desktop status is now: NodeHasSufficientMemory     
  Normal  NodeHasNoDiskPressure    37m (x8 over 37m)  kubelet          Node docker-desktop status is now: NodeHasNoDiskPressure       
  Normal  NodeHasSufficientPID     37m (x7 over 37m)  kubelet          Node docker-desktop status is now: NodeHasSufficientPID        
  Normal  NodeAllocatableEnforced  37m                kubelet          Updated Node Allocatable limit across pods
  Normal  RegisteredNode           37m                node-controller  Node docker-desktop event: Registered Node docker-desktop in Controller

early@JAKEPARK-MAINPC MINGW64 ~
$kubectl cluster-info
Kubernetes control plane is running at https://kubernetes.docker.internal:6443
CoreDNS is running at https://kubernetes.docker.internal:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

early@JAKEPARK-MAINPC MINGW64 ~
$kubectl config current-context
docker-desktop

early@JAKEPARK-MAINPC MINGW64 ~
$kubectl get namespaces
NAME              STATUS   AGE
default           Active   22h
kube-node-lease   Active   22h
kube-public       Active   22h
kube-system       Active   22h

early@JAKEPARK-MAINPC MINGW64 ~
$kubectl get all -n kube-system
NAME                                         READY   STATUS    RESTARTS   AGE
pod/coredns-66bc5c9577-f4f4z                 1/1     Running   2          22h
pod/coredns-66bc5c9577-mvtr4                 1/1     Running   2          22h
pod/etcd-docker-desktop                      1/1     Running   2          22h
pod/kube-apiserver-docker-desktop            1/1     Running   2          22h
pod/kube-controller-manager-docker-desktop   1/1     Running   2          22h
pod/kube-proxy-jvffh                         1/1     Running   2          22h
pod/kube-scheduler-docker-desktop            1/1     Running   2          22h
pod/storage-provisioner                      1/1     Running   3          22h
pod/vpnkit-controller                        1/1     Running   2          22h

NAME               TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns   ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP,9153/TCP   22h

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/kube-proxy   1         1         1       1            1           kubernetes.io/os=linux   22h

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns   2/2     2            2           22h

NAME                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-66bc5c9577   2         2         2       22h

early@JAKEPARK-MAINPC MINGW64 ~
$
