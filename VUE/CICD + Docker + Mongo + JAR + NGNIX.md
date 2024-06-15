
### Prerequisites

1. **GitLab Account**: Ensure you have a GitLab account and a project repository.
2. **Docker**: Make sure Docker is installed on your machine and on the target server.
3. **SSH Access**: Ensure you have SSH access to the target server.
4. **Spring Boot Project**: A backend project in Spring Boot.
5. **Frontend Application**: A frontend application to be served by NGINX.
6. **MongoDB**: MongoDB container for database purposes.

### Step 1: Set Up Your Spring Boot Backend

1. **Create a Spring Boot Application**: Use Spring Initializr to create a new Spring Boot project with Maven.

2. **Dockerfile for Spring Boot**:
   Create a `Dockerfile` in the root of your Spring Boot project.

   ```dockerfile
   FROM openjdk:11-jre-slim
   ARG JAR_FILE=target/*.jar
   COPY ${JAR_FILE} app.jar
   ENTRYPOINT ["java","-jar","/app.jar"]
   ```

3. **Maven Configuration**:
   Ensure your `pom.xml` is correctly set up to build a JAR file.

### Step 2: Set Up Your Frontend Application

1. **Create NGINX Configuration**: Create an NGINX configuration file `nginx.conf` to serve your frontend application.

   ```nginx
   server {
       listen 80;
       server_name localhost;

       location / {
           root /usr/share/nginx/html;
           index index.html index.htm;
       }

       location /api {
           proxy_pass http://backend:8080;
       }
   }
   ```

2. **Dockerfile for NGINX**:
   Create a `Dockerfile` in your frontend project directory.

   ```dockerfile
   FROM nginx:alpine
   COPY dist/ /usr/share/nginx/html
   COPY nginx.conf /etc/nginx/nginx.conf
   ```

### Step 3: Set Up MongoDB

1. **MongoDB Docker Configuration**:
   No specific Dockerfile is needed. We will use the official MongoDB Docker image.

### Step 4: CI/CD Configuration in GitLab

1. **GitLab CI/CD Configuration**:
   Create a `.gitlab-ci.yml` file in the root of your project. This file will handle building the Docker images, saving them as tar files, transferring them to the target server, and running them there.

   ```yaml
   stages:
     - build
     - test
     - save
     - deploy

   variables:
     MAVEN_CLI_OPTS: "--batch-mode --errors --fail-at-end --show-version"
     DOCKER_DRIVER: overlay2
     SSH_PRIVATE_KEY: $SSH_PRIVATE_KEY
     TARGET_SERVER: $TARGET_SERVER
     TARGET_USER: $TARGET_USER

   build-backend:
     stage: build
     image: maven:3.6.3-jdk-11
     script:
       - cd backend
       - mvn $MAVEN_CLI_OPTS package
       - cd ..
       - docker build -t backend:latest ./backend

   build-frontend:
     stage: build
     image: node:14
     script:
       - cd frontend
       - npm install
       - npm run build
       - cd ..
       - docker build -t frontend:latest ./frontend

   save-images:
     stage: save
     image: docker:latest
     services:
       - docker:dind
     script:
       - docker save -o backend.tar backend:latest
       - docker save -o frontend.tar frontend:latest
     artifacts:
       paths:
         - backend.tar
         - frontend.tar

   test-backend:
     stage: test
     image: maven:3.6.3-jdk-11
     script:
       - cd backend
       - mvn $MAVEN_CLI_OPTS test

   deploy:
     stage: deploy
     image: alpine:latest
     before_script:
       - apk add --no-cache openssh
       - mkdir -p ~/.ssh
       - echo "$SSH_PRIVATE_KEY" | tr -d '\r' > ~/.ssh/id_rsa
       - chmod 600 ~/.ssh/id_rsa
       - ssh-keyscan -H $TARGET_SERVER >> ~/.ssh/known_hosts
     script:
       - scp backend.tar frontend.tar $TARGET_USER@$TARGET_SERVER:/tmp/
       - ssh $TARGET_USER@$TARGET_SERVER 'docker load -i /tmp/backend.tar'
       - ssh $TARGET_USER@$TARGET_SERVER 'docker load -i /tmp/frontend.tar'
       - ssh $TARGET_USER@$TARGET_SERVER 'docker run -d --name mongodb -p 27017:27017 mongo:latest'
       - ssh $TARGET_USER@$TARGET_SERVER 'docker run -d --name backend --link mongodb -p 8080:8080 backend:latest'
       - ssh $TARGET_USER@$TARGET_SERVER 'docker run -d --name frontend --link backend -p 80:80 frontend:latest'
   ```

### Step 5: Running the CI/CD Pipeline

1. **Commit and Push**: Commit your changes and push them to your GitLab repository. GitLab will automatically trigger the CI/CD pipeline.

2. **Check Pipeline Status**: Go to your GitLab project and check the pipeline status under the CI/CD section.

### Explanation of the Pipeline

- **Build Stage**: Builds Docker images for the backend and frontend applications.
- **Test Stage**: Runs tests for the backend application.
- **Save Stage**: Saves the Docker images to tar files and keeps them as artifacts.
- **Deploy Stage**:
  - Sets up SSH access.
  - Transfers the tar files to the target server using SCP.
  - Loads the Docker images on the target server.
  - Runs MongoDB, backend, and frontend containers on the target server.
