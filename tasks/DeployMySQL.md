### Deploy MySQL on Kubernetes	

* Create secrets first to reference in deployment further.
```
kubectl create secret generic mysql-root-pass \
  --from-literal=password=YUIidhb667
kubectl create secret generic mysql-user-pass \
  --from-literal=username=kodekloud_sam \
  --from-literal=password=Rc5C9EyvbU
kubectl create secret generic mysql-db-url \
  --from-literal=database=kodekloud_db3

```
* YAML files to create PersistentVolume, PersistentVolumeClaim, Service and Deployment with appropriate environment variables which will use above created secrets
```
apiVersion: v1
kind: Service
metadata:
  name: mysql
  labels:
    app: mysql-app
spec:
  type: NodePort
  ports:
    - port: 3306
      nodePort: 30007
  selector:
    app: mysql-app
    tier: mysql
  
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
  labels:
    app: mysql-app
spec:
  storageClassName: manual
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  labels:
    app: mysql-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  labels:
    app: mysql-app
spec:
  selector:
    matchLabels:
      app: mysql-app
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql-app
        tier: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-root-pass
              key: password
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: mysql-db-url
              key: database
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim

```
