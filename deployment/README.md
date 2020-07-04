# Deployment

## Docker
### Create a docker image
```bash
docker build -t reckue/post:latest .
```

### Push image to Docker Hub
```bash
docker push reckue/post:latest
```

## Deploy with Kubernates

**deploy.yaml**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: post
  name: post
spec:
  replicas: 1
  selector:
    matchLabels:
      app: post
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: post
    spec:
      containers:
      - image: reckue/post:latest
        name: post
        resources: {}
status: {}
---
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: post
  name: post
spec:
  ports:
  - name: 8080-8080
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: post
  type: ClusterIP
status:
  loadBalancer: {}
```

### Create deployment
```bash
oc create -f config/k8s/deploy.yaml
```

### Create deployment with docker image
```bash
kubectl create deployment post --image=reckue/post:latest --dry-run -o=yaml > deployment.yaml
```

### Create service and open port
```bash
kubectl create service clusterip post --tcp=8080:8080 --dry-run -o=yaml >> deployment.yaml
```
