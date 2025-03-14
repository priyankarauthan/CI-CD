# CI-CD



# ✅ Deployment Workflow

### 1️⃣ Push the Code to GitLab

Developers commit & push code to a GitLab repository.
GitLab CI/CD pipeline can be triggered automatically.

### 2️⃣ Build a JAR using Maven/Gradle

GitLab CI/CD pipeline builds the JAR using Maven or Gradle.
Example Maven command:
sh
Copy
Edit
mvn clean package
Output: A JAR file (target/my-app.jar).

### 3️⃣ Build a Docker Image

Use a Dockerfile to create a Docker image containing the JAR.
Example Dockerfile:
dockerfile

FROM openjdk:17
COPY target/my-app.jar /app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
Build the image:
sh

docker build -t my-app:latest .
Store the image in a registry (Docker Hub, AWS ECR, or an on-premise registry):
sh

docker tag my-app my-dockerhub-username/my-app:latest
docker push my-dockerhub-username/my-app:latest

### 4️⃣ Deploy the Docker Container

The Docker container is run on a server (AWS, on-prem, etc.).
Example:
sh
docker run -d -p 8080:8080 --name my-app my-dockerhub-username/my-app:latest
If using Kubernetes, deploy it via kubectl apply -f deployment.yaml.




## How do you do deployment in our company?

Deployment processes vary from company to company, but since you have worked with Spring Boot, Kafka, AWS S3, Kubernetes (K8s), DB2, Perl, and Elasticsearch, your company likely follows a CI/CD pipeline-based deployment for Java microservices.

Could you confirm which specific deployment strategy your company follows? Here are some possible options:

### 1. CI/CD-Based Deployment (Jenkins, GitHub Actions, GitLab CI/CD, etc.)

Code Commit → Developer pushes changes to Git (GitHub, GitLab, Bitbucket).
Build & Test → A CI tool like Jenkins, GitHub Actions, GitLab CI builds the application using Maven/Gradle and runs unit/integration tests.
Artifact Storage → The built JAR/WAR is stored in Nexus, Artifactory, or AWS S3.
Deployment to Kubernetes/Docker
A Docker image is created and pushed to Docker Hub or AWS ECR.
Helm charts or Kubernetes manifests deploy the service to K8s clusters.
Monitoring & Logging → Services like Prometheus, Grafana, Splunk, ELK (Elasticsearch, Logstash, Kibana) monitor logs & metrics.


### 2. Blue-Green Deployment (Zero Downtime)

Two environments:
Blue → Running production version.
Green → New deployment.
Traffic is switched to the green environment after successful testing.
Used with AWS ALB, Nginx, Istio, or Kubernetes Ingress Controllers.

### 3. Canary Deployment (Gradual Rollout)

New version is released to a small percentage of users first.
If no issues, traffic is gradually increased.
Achieved using Kubernetes, Istio, Argo Rollouts.

### 4. Manual Deployment (Legacy Systems with DB2 & Perl Jobs)

For DB2, Perl-based scripts:
Files are copied to a staging area (e.g., NFS, HDFS).
Jobs are manually triggered using cron jobs or batch jobs.
Logs are stored in Splunk or Elasticsearch.
Questions for You:
Are you using Jenkins, GitHub Actions, or GitLab CI/CD for deployment?
Are your microservices deployed in Kubernetes (K8s) or on AWS ECS/EC2?
Do you use Docker & Helm for containerization?
Are you implementing blue-green or canary deployments?
Let me know, and I can provide more specific details based on your workflow! 🚀


## Artifactory in Deployment

Artifactory is a binary artifact repository used for storing and managing build artifacts, such as JARs, WARs, Docker images, and other dependencies. It is commonly used in CI/CD pipelines for deploying Java applications.


     
