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

# MongoDB
Please follow this tutorial:
https://www.melvinvivas.com/converting-a-mongodb-docker-compose-file-to-a-kubernetes-deployment/

## Step 1. Create docker-compose.yml
```yaml
version: '3'
services:
  mongodb:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - "mongodb:/data/db"
    networks:
      - network1

volumes:
  mongodata:

networks:
  network1:
```

## Step 2. Generate kubernates scripts
```
kompose convert -f docker-compose.yml
```

## Step 3. Create PVC, Deployment and Service
```
kubectl create -f mongodata-persistentvolumeclaim.yaml
kubectl create -f mongodb-deployment.yaml
kubectl create -f mongodb-service.yaml
```
