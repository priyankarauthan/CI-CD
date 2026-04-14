# CI-CD 

- [How do you do deployment in your company?](#how-do-you-do-deployment-in-your-company)
- [How does Docker work across all OS?](#how-does-docker-work-across-all-os)
- [Docker Architecture](#docker-architecture)
- [ What is Port Mapping in Docker](#what-is-port-mapping-in-docker)
- [🚀 Step-by-Step: Run Spring Boot App in Docker](#run-spring-boot-app-in-docker)



## What is Port Mapping in Docker?

Port mapping means connecting a port inside a container to a port on your machine (host) so you can access the application.

## Step-by-Step: Run Spring Boot App in Docker


✅ 1. Build your Spring Boot JAR   

First, create a JAR file of your application.

If using Maven:

mvn clean package

If using Gradle:

gradle build

👉 Output will be inside:

target/your-app.jar   
✅ 2. Create a Dockerfile   

In your project root directory, create a file named:   

Dockerfile   
Example Dockerfile:  
```
**Use base image with Java**   
FROM openjdk:17-jdk-slim         

** Set working directory inside container**   
WORKDIR /app   

** Copy jar file from local to container **   
COPY target/your-app.jar app.jar   

** Expose application port **   
EXPOSE 8080   

** Command to run the application **   
ENTRYPOINT ["java", "-jar", "app.jar"]
```     
✅ 3. Build Docker Image      

Run this command in your project root (where Dockerfile exists):

docker build -t springboot-app:1.0 .   

👉 This will:   

Read Dockerfile   

Create image   

Tag it as springboot-app:1.0      

✅ 4. Run Docker Container   
docker run -d -p 8080:8080 springboot-app:1.0
Explanation:   

-d → run in background   

-p 8080:8080 → map local port → container port   

✅ 5. Verify Application   

Open browser:

http://localhost:8080

If deployed correctly → your app will be running 🎉

✅ 6. Check Running Containers   
docker ps
✅ 7. Stop Container   
docker stop <container_id>   


## What is a Container?

A container is a lightweight package that includes:

- Application code

- Runtime (Java, Python, Node)

- Libraries & dependencies

- Config files

👉 All bundled together so it runs anywhere consistently


## 🔹 Real Tools

- Docker → to create containers

- Kubernetes → to manage containers at scale

| Tool       | Responsibility           |
| ---------- | ------------------------ |
| Jenkins    | Automates steps          |
| Docker     | Builds & runs containers |
| Kubernetes | Deploys containers       |



## 🐳 Docker Architecture 

👉 Think of Docker as having 3 main parts:
```
You (CLI command)
   ↓
Docker CLI
   ↓
Docker Daemon (server)
   ↓
Containers / Images created
```

**🧩 1. Docker CLI (Command Line)**

👉 This is what you use

Example:

docker build,   docker run,      docker ps

👉 It’s just a tool to give instructions

**🧠 2. Docker Engine (Brain of Docker)**

👉 This is the main system that does all the work

It:

- Builds images

- Runs containers

- Manages everything

👉 You don’t see it, but it runs in background

**📦 3. Images (Blueprint)**

👉 Image = ready-made package

Contains:

App

Java/Python

Dependencies

👉 Example:
```
docker build -t my-app .
```
**🚀 4. Containers (Running App)**

👉 Container = running version of image

Example:

docker run my-app

👉 This actually starts your app

## 🔄 Full Flow   
1. You type command (CLI)
2. Docker Engine receives it
3. Engine uses Image
4. Creates Container
5. App starts  




        ┌──────────────┐
        │    USER      │
        │ (You / Dev)  │
        └──────┬───────┘
               │
               ▼
        ┌──────────────┐
        │ Docker CLI   │
        │ (docker run) │
        └──────┬───────┘
               │
               ▼
        ┌──────────────┐
        │ REST API     │
        │ (Communication)
        └──────┬───────┘
               │
               ▼
        ┌──────────────┐
        │ Docker Engine│
        │ (dockerd)    │  ← SERVER
        └──────┬───────┘
               │
     ┌─────────┼─────────┐
     ▼         ▼         ▼
┌────────┐ ┌────────┐ ┌────────┐
│ Images │ │Containers│ │Networks│
└────────┘ └────────┘ └────────┘

## 🔥 What Happens Internally In Docker

When you run: docker run my-app

👉 Docker Engine: 
- Checks if image exists

- Creates container

- Runs your app

## How does Docker work across all OS?

**👉 Docker containers need Linux to run**

❓ Then your question becomes:

👉 “If my laptop is Mac/Windows (not Linux), how does Docker still work?”

🔥 Now I’ll explain in the simplest way    
**🐧 Case 1: If you are using LINUX**

👉 Your system is already Linux

So:

Docker runs directly

Containers run directly

👉 No extra layer needed

Think:-

👉 You already have what Docker needs

**🍎🪟 Case 2: If you are using MAC or WINDOWS** 

👉 Your system is NOT Linux ❌

👉 But Docker NEEDS Linux ✅

💡 So what Docker does?

👉 It secretly creates a small Linux system inside your machine

Step-by-step:

You install Docker Desktop

Docker creates a small Linux VM (in background)

Containers run inside that Linux

So actually:

👉 When you run:

docker run my-app

👉 It is doing:

Your Laptop (Mac/Windows)
    ↓
Small Hidden Linux
    ↓
Your Container runs here





## 📦 What Exactly Happens in Containerization (Simple Steps)

Think of it in 2 parts:

👉 1. Build (prepare your app)       
👉 2. Run (start your app)       

🏗️ PART 1: BUILD (Creating the Image)   
**🔹 Step 1: You write your app**   

Example:

Spring Boot app → app.jar

**🔹 Step 2: You write a Dockerfile**   
```
FROM openjdk:17
COPY app.jar app.jar
CMD ["java","-jar","app.jar"]
```

👉 This file tells Docker:

Use Java

Copy my app

Run my app

**🔹 Step 3: You build the image**
docker build -t my-app .

## 👉 What Docker does:

- Takes base image (Java already installed)

- Adds your app (app.jar)

- Saves everything as a package

👉 This package = Image

🔥 Think of Image as:

👉 A ready-made setup (like a zipped file with everything)

## 🚀 PART 2: RUN (Starting the Container)
**🔹 Step 4: You run the container**
docker run my-app
**🔹 Step 5: Docker prepares environment**

👉 Docker:

Creates a small isolated space

Gives your app its own:

Files

Network

Processes

**🔹 Step 6: No OS is started**

👉 Important:

❌ No new OS

✅ Uses your system’s OS

👉 That’s why it’s fast

**🔹 Step 7: Your app starts**

👉 Docker runs:
```
java -jar app.jar
```
👉 Your app is now:

Running

Accessible (API, service, etc.)

## 🔁 Full Flow (Very Simple)    
Write App → Create Dockerfile → Build Image → Run Container → App Starts








## ⚙️ What Goes Into a Jenkins Groovy (Jenkinsfile) for Microservices?

Think of Jenkins as the orchestrator of your microservices lifecycle:
```
Code → Build → Test → Package → Scan → Deploy → Verify
```


## 🧱 Ideal Pipeline Stages for Microservices    

🔹 1. Checkout Stage (Get Code)   
```
stage('Checkout') {
    steps {
        git 'https://github.com/repo.git'
    }
}
```

👉 Pull latest code from Git

🔹 2. Build Stage          
```
stage('Build') {
    steps {
        sh 'mvn clean compile'
    }
}
```

👉 Compile your microservice

🔹 3. Unit Test Stage       
```
stage('Unit Test') {
    steps {
        sh 'mvn test'
    }
}
```
👉 Run unit tests
👉 Fail fast if broken

🔹 4. Code Quality / Static Analysis (Very Important 🔥)       
```
stage('Code Quality') {
    steps {
        sh 'mvn sonar:sonar'
    }
}
```
👉 Use tools like:

SonarQube
👉 Ensures clean code

🔹 5. Package Stage    
```
stage('Package') {
    steps {
        sh 'mvn clean package'
    }
}
```
👉 Creates JAR/WAR    

🔹 6. Build Docker Image (Microservices Core Step)    
```
stage('Docker Build') {
    steps {
        sh 'docker build -t my-service:latest .'
    }
}
```

👉 Containerization happens here

🔹 7. Security Scan (Advanced & Important)    
```
stage('Security Scan') {
    steps {
        sh 'trivy image my-service:latest'
    }
}
```
👉 Scan for vulnerabilities

🔹 8. Push Image to Registry    
```
stage('Push Image') {
    steps {
        sh 'docker push my-service:latest'
    }
}
```

👉 Store image in:

Docker Hub / ECR / GCR

🔹 9. Deploy Stage (Kubernetes)    
```
stage('Deploy') {
    steps {
        sh 'kubectl apply -f deployment.yaml'
    }
}
```

👉 Deploy microservice to cluster

🔹 10. Integration Test / Smoke Test    
```
stage('Smoke Test') {
    steps {
        sh 'curl http://service/health'
    }
}
```

👉 Check if service is running

🔹 11. Notification Stage    
```
post {
    success {
        echo 'Deployment successful'
    }
    failure {
        echo 'Deployment failed'
    }
}
```
## 🔥 Ideal Pipeline Flow (Microservices)    
```
Checkout
   ↓
Build
   ↓
Unit Test
   ↓
Code Quality
   ↓
Package
   ↓
Docker Build
   ↓
Security Scan
   ↓
Push Image
   ↓
Deploy (K8s)
   ↓
Smoke Test
   ↓
Notify

```


## 🧠 Microservices-Specific Considerations    

✅ 1. Independent Pipelines

Each microservice has its own Jenkinsfile

✅ 2. Parallel Execution (Advanced)
stage('Parallel Tests') {
    parallel {
        stage('Unit Test') {
            steps { sh 'mvn test' }
        }
        stage('Integration Test') {
            steps { sh 'mvn verify' }
        }
    }
}
✅ 3. Environment-Based Deployment

Dev → QA → UAT → Prod

✅ 4. Versioning

Tag images:

my-service:v1.0.0
✅ 5. Rollback Strategy

Keep previous versions ready

## 🚫 Common Mistakes

❌ Skipping tests

❌ No security scanning

❌ No rollback strategy

❌ One pipeline for all services

❌ No health checks

## 🎯 Interview Answer (Perfect)

In a microservices architecture, the Jenkins pipeline typically includes stages like code checkout, build, unit testing, static code analysis, packaging, Docker image creation, security scanning, pushing the image to a registry, deployment to Kubernetes, and post-deployment validation like smoke tests. Each microservice has its own independent pipeline, enabling isolated builds and deployments.



## Steps to Automate Deployment in GitLab

1️⃣ Push Code to GitLab

Developers commit and push code to the GitLab repository.

2️⃣ Build the JAR using Maven/Gradle

The GitLab pipeline compiles the Java code and creates a JAR.

3️⃣ Build a Docker Image & Push to Registry

The pipeline creates a Docker image and pushes it to a registry (Docker Hub, AWS ECR, GitLab Container Registry, etc.).

4️⃣ Deploy the Docker Container on a Server

The pipeline pulls the latest image and runs it on a remote server (AWS EC2, On-Premise VM, Kubernetes, etc.).





## How do you do deployment in your company?

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

## How do you ensure the quality of your code?


##### ✅ 1. In Your IDE (e.g., IntelliJ IDEA, Eclipse)

a. Warnings and Annotations

Deprecated methods are usually highlighted or struck through.

Look for the @Deprecated annotation above the method or class.
```
@Deprecated
public void oldMethod() {
    // ...
}
```
b. Hover or Ctrl+Click

Hover over or Ctrl/Cmd+Click the method to see the Javadoc which often includes:

A warning.

A recommendation for the alternative method.

c. IDE Inspection Tools
In IntelliJ IDEA:
Code > Inspect Code > Whole Project → will list deprecated API usages.

In Eclipse:
Use Problems view and filter for deprecation.

✅ 2. Use Build Tool Warnings

a. Maven
Use mvn clean compile with -X for debug logs. It shows deprecated warnings.

b. Gradle
Run: ./gradlew build --warning-mode all

✅ 3. Static Analysis Tools

SonarQube, Checkstyle, and PMD can detect deprecated API usage.

They help flag usage in reports and CI pipelines.

✅ 4. Dependency Upgrade Awareness

When you upgrade Spring Boot, check the Spring Boot release notes and Spring Framework deprecated list for deprecations.

✅ 5. Using jdeprscan (JDK Tool)

If you're using Java 9+, use the jdeprscan tool:

```
jdeprscan --class-path target/classes --release 17
```
This reports use of deprecated APIs for the given Java release.

     
