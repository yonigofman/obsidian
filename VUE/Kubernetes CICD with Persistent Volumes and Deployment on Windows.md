### Full Tutorial on Kubernetes CICD with Persistent Volumes and Deployment on Windows

#### Introduction
This tutorial covers the deployment of a MongoDB application on Kubernetes with persistent storage and a Continuous Integration/Continuous Deployment (CICD) pipeline for backend and frontend applications using GitLab CI. It includes setting up PersistentVolumeClaims (PVC) in Kubernetes, defining deployments, and automating build and deployment processes using a GitLab CI pipeline.

#### Prerequisites
- Kubernetes cluster
- kubectl configured to access your cluster
- GitLab runner configured to execute CI/CD pipelines
- Basic knowledge of Kubernetes, YAML, and GitLab CI

#### Step 1: Setting Up Persistent Volumes

**PersistentVolumeClaim (PVC)**
A PVC is used to request persistent storage for your pods. The PVC abstracts the underlying storage and allows Kubernetes to bind it to a suitable PersistentVolume (PV).

**Example PVC YAML Configuration (mongo-pvc.yaml):**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

**How It Works:**
1. **PVC Creation:** When you apply the `mongo-pvc.yaml`, Kubernetes will look for a PV that meets the storage request (1Gi) and access mode (ReadWriteOnce).
2. **PVC Binding:** If a suitable PV is found, the PVC is bound to it.

#### Step 2: Kubernetes Deployment with Persistent Volumes

**Example Deployment YAML Configuration (mongo-deployment.yaml):**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      labels:
        app: mongo
    spec:
      containers:
      - name: mongo
        image: mongo:latest
        ports:
        - containerPort: 27017
        volumeMounts:
        - name: mongo-storage
          mountPath: /data/db
      volumes:
      - name: mongo-storage
        persistentVolumeClaim:
          claimName: mongo-pvc
```

**Explanation:**
- **volumeMounts:** Specifies the volume mount details inside the MongoDB container.
- **volumes:** Defines the volume bound to the PVC (`mongo-pvc`).

#### Step 3: Applying the Configuration
To apply the configuration files, run:
```sh
kubectl apply -f mongo-pvc.yaml
kubectl apply -f mongo-deployment.yaml
```

This ensures the PVC is created and available when the deployment is initiated.

#### Step 4: Setting Up GitLab CI for CICD

**GitLab CI/CD Configuration (gitlab-ci.yml):**
```yaml
stages:
  - build-backend
  - build-frontend
  - deploy

build-backend:
  stage: build-backend
  image: maven:3.8.1-jdk-11
  script:
    - echo "Building backend with Maven"
    - mvn clean package
  artifacts:
    paths:
      - target/*.jar
    expire_in: 1 hour

build-frontend:
  stage: build-frontend
  image: node:14
  script:
    - echo "Building frontend with npm"
    - cd frontend
    - npm install
    - npm run build
  artifacts:
    paths:
      - frontend/dist
    expire_in: 1 hour

deploy:
  stage: deploy
  image: mcr.microsoft.com/windows/servercore:ltsc2022
  before_script:
    - apt-get update && apt-get install -y sshpass
    - echo "alias on_server=\"sshpass -p \$USER_PASSWORD ssh -o StrictHostKeyChecking=no \$USER_NAME@\$SERVER_IP\"" >> ~/.bashrc
    - source ~/.bashrc
  script:
    - echo "Deploying to Kubernetes"
    - on_server 'kubectl set image deployment/backend backend=${SERVER_IP}/backend:latest'
    - on_server 'kubectl set image deployment/frontend frontend=${SERVER_IP}/frontend:latest'
    - on_server 'kubectl apply -f k8s/mongo-deployment.yaml'
  environment:
    name: production
    url: https://${SERVER_IP}
```

**Explanation:**
1. **build-backend:** Uses a Maven image to build the backend Java application.
2. **build-frontend:** Uses a Node.js image to build the frontend application.
3. **deploy:** Uses a Windows Server image to deploy the applications to Kubernetes. It includes commands to set the deployment images and apply the deployment configuration.

#### Summary
- **Persistent Storage Setup:** Utilize PVC to provide persistent storage for MongoDB.
- **Kubernetes Deployment:** Define volume mounts and deployment configurations for MongoDB.
- **CI/CD Pipeline:** Automate build and deployment processes using GitLab CI with stages for building and deploying both backend and frontend applications.

By following this tutorial, you can ensure your Kubernetes deployments have persistent storage and automate the deployment process through CI/CD pipelines.