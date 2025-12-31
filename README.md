# p-14653-1-mission
- 0004 완료

<img width="1505" height="1116" alt="image" src="https://github.com/user-attachments/assets/7fd42dfe-6885-495b-8cc1-7ae1f3e79053" />

  
early@JAKEPARK-MAINPC MINGW64 ~
$ vi nginx-pod.yaml

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-pod.yaml
pod/nginx-pod created

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl apply -f nginx-pod.yaml
pod/nginx-pod unchanged

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pods -o wide
NAME        READY   STATUS    RESTARTS   AGE   IP          NODE             NOMINATED NODE   READINESS GATES
nginx-pod   1/1     Running   0          33s   10.1.0.15   docker-desktop   <none>           <none>

early@JAKEPARK-MAINPC MINGW64 ~
$ kubectl get pod nginx-pod -o yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"nginx","environment":"dev"},"name":"nginx-pod","namespace":"default"},"spec":{"containers":[{"image":"nginx:1.25","name":"nginx","ports":[{"containerPort":80}],"resources":{"limits":{"cpu":"200m","memory":"128Mi"},"requests":{"cpu":"100m","memory":"64Mi"}}}]}}
  creationTimestamp: "2025-12-31T07:06:12Z"
  generation: 1
  labels:
    app: nginx
    environment: dev
  name: nginx-pod
  namespace: default
  resourceVersion: "98773"
  uid: 7228853b-89fb-4553-abef-4686d4c18c27
spec:
  containers:
  - image: nginx:1.25
    imagePullPolicy: IfNotPresent
    name: nginx
    ports:
    - containerPort: 80
      protocol: TCP
    resources:
      limits:
        cpu: 200m
        memory: 128Mi
      requests:
        cpu: 100m
        memory: 64Mi
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-4cds4
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: docker-desktop
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-4cds4
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2025-12-31T07:06:21Z"
    observedGeneration: 1
    status: "True"
    type: PodReadyToStartContainers
  - lastProbeTime: null
    lastTransitionTime: "2025-12-31T07:06:12Z"
    observedGeneration: 1
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2025-12-31T07:06:21Z"
    observedGeneration: 1
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2025-12-31T07:06:21Z"
    observedGeneration: 1
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2025-12-31T07:06:12Z"
    observedGeneration: 1
    status: "True"
    type: PodScheduled
  containerStatuses:
  - allocatedResources:
      cpu: 100m
      memory: 64Mi
    containerID: docker://5a2d60b20eca6a8105aab486d6440aab2417c947e5048fe270705fc0eeea4ecb
    image: nginx:1.25
    imageID: docker-pullable://nginx@sha256:a484819eb60211f5299034ac80f6a681b06f89e65866ce91f356ed7c72af059c
    lastState: {}
    name: nginx
    ready: true
    resources:
      limits:
        cpu: 200m
        memory: 128Mi
      requests:
        cpu: 100m
        memory: 64Mi
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2025-12-31T07:06:21Z"
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-4cds4
      readOnly: true
      recursiveReadOnly: Disabled
  hostIP: 192.168.65.3
  hostIPs:
  - ip: 192.168.65.3
  observedGeneration: 1
  phase: Running
  podIP: 10.1.0.15
  podIPs:
  - ip: 10.1.0.15
  qosClass: Burstable
  startTime: "2025-12-31T07:06:12Z"

early@JAKEPARK-MAINPC MINGW64 ~
$kubectl delete -f nginx-pod.yaml
pod "nginx-pod" deleted from default namespace

early@JAKEPARK-MAINPC MINGW64 ~
$
