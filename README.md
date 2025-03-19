# CI-CD

# Steps to Automate Deployment in GitLab

1️⃣ Push Code to GitLab

Developers commit and push code to the GitLab repository.

2️⃣ Build the JAR using Maven/Gradle

The GitLab pipeline compiles the Java code and creates a JAR.

3️⃣ Build a Docker Image & Push to Registry

The pipeline creates a Docker image and pushes it to a registry (Docker Hub, AWS ECR, GitLab Container Registry, etc.).

4️⃣ Deploy the Docker Container on a Server

The pipeline pulls the latest image and runs it on a remote server (AWS EC2, On-Premise VM, Kubernetes, etc.).





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


     
