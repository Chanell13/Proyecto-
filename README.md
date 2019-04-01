```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: acmeexplorer-deployment
  labels:
    app: acmeexplorer
spec:
  selector:
    matchLabels:
      app: acmeexplorer
  template:
    metadata:
      labels:
        app: acmeexplorer
    spec:
      containers:
        - name: acmeexplorer
          image: favsol26/do1819-02
          ports:
            - containerPort: 8080
              name: http-port
          env:
            - name: SERVICE_NAME
              value: app
            - name: DB_URI
              value: mongodb://mongodb-svc:27017/DB1
            - name: mongoDBHostname
              value: "mongodb-svc"
```
                
```yaml          
apiVersion: v1
kind: Service
metadata:
  name: acmeexplorersvc
  labels:
    app: acmeexplorer
spec:
  selector:
    app: acmeexplorer
  ports:
  - name: http-svc-port
    port: 8080
    targetPort: http-port
    nodePort: 30082
  type: NodePort
```
