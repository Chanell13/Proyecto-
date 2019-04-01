# Deploy a MongoDB

## 1)Create the headless service configuration file.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongo-headless-service
  labels:
    app: mongodb
spec:
  selector:
    app: mongodb
  ports:
  - port: 27017
    targetPort: db-port
  type: ClusterIP
```

## 2) Create the deploy configuration file.
```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: mongo-statefulset
  labels:
    app: mongodb
spec:
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
        - name: mongodb
          image: mongo
          ports:
            - containerPort: 27017
              name: db-port
```			  

## 3)  Deploy the Service
```bash
$ kubectl apply -f mongo-headless-service.yaml
service "mongo" created
```

## 4)  Deploy the Service
```bash
$ kubectl apply -f mongo-statefulset.yaml
statefulset "mongo" created
```

## 5) Verify the service and deploy.
```bash
$ kubectl get service mongo
NAME    TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)     AGE
mongo   ClusterIP   None         <none>        27017/TCP   5s
```

```bash
$ kubectl get statefulset mongo
NAME    DESIRED   CURRENT   AGE
mongo   3         3         1m
```
## 5) Verify logs.
```bash
$ kubectl logs mongo
```
