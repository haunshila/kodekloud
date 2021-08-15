### Kubernetes Time Check Pod	

* Create a 'nautilus' namespace if its not there
```
kubectl create namespace nautilus
```
* yaml file for pod
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: time-config
  namespace: nautilus
data:
  TIME_FREQ: "11"
---
apiVersion: v1
kind: Pod
metadata:
  name: time-check
  namespace: nautilus
  labels:
    app: time-check
spec:
  volumes:
    - name: log-volume
      emptyDir: {}
  containers:
    - name: time-check
      image: busybox:latest
      volumeMounts:
        - mountPath: /opt/dba/time
          name: log-volume
      env:
        - name: TIME_FREQ
          valueFrom: 
            configMapKeyRef:
                name: time-config
                key: TIME_FREQ
      command: ["/bin/sh", "-c"]
      args:
        [
          "while true; do date; sleep $TIME_FREQ;done > /opt/dba/time/time-check.log",
        ]


```

* update above yaml as suggested in task
