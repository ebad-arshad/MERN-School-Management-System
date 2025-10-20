# 🏫 MERN School Management System — DevOps Edition

> 🚀 A full-featured **MERN (MongoDB, Express, React, Node.js)** application integrated with **Docker**, **Jenkins CI/CD**, and **Kubernetes** for production-grade deployment.

---

## 📘 Table of Contents
- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [DevOps Features](#devops-features)
- [Project Structure](#project-structure)
- [How to Run with Docker](#how-to-run-with-docker)
- [Environment Variables](#environment-variables)
- [CI/CD Pipeline (Jenkins)](#cicd-pipeline-jenkins)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Future Enhancements](#future-enhancements)
- [Author](#author)

---

## 🧩 Project Overview

This project is a **School Management System** built using the MERN stack — providing functionality for managing students, teachers, and classes.
It has been **containerized**, **automated**, and **orchestrated** to showcase modern **DevOps pipelines** from development to deployment.

---

## 🛠 Tech Stack

| Layer | Tool/Framework |
|-------|----------------|
| Frontend | React.js |
| Backend | Node.js + Express |
| Database | MongoDB |
| Containerization | Docker |
| CI/CD | Jenkins |
| Orchestration | Kubernetes |
| Cloud Registry | Docker Hub |

---

## ⚙️ DevOps Features

✅ **Dockerized** each service (frontend, backend, database)  
✅ **Docker Compose** integration for local orchestration  
✅ **Jenkins CI/CD pipeline** for automatic build, test, and deploy  
✅ **Kubernetes manifests** for production-grade deployment  
✅ **Resource limits, HPA (Horizontal Pod Autoscaler)**, and **stress testing** implemented  
✅ Clean, modular repo structure under `/k8s`  

---

## 📁 Project Structure

```
MERN-School-Management-System/
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   └── server.js
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   └── src/
├── docker-compose.yaml
├── Jenkinsfile
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── hpa.yaml
│   └── mongo-pv.yaml
└── README.md
```

---

## 🐳 How to Run with Docker

Follow these simple steps to run the project locally using Docker and Docker Compose 👇

### 🧰 Prerequisites
Make sure you have the following installed:
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)
- (Optional) [Git](https://git-scm.com/)

---

### ⚡ Step 1: Clone the Repository

```bash
git clone https://github.com/ebad-arshad/MERN-School-Management-System.git
cd MERN-School-Management-System
```

---

### ⚡ Step 2: Configure Environment Variables

Create a `.env` file in the project root (or inside `/backend`) with:

```bash
MONGO_URI=mongodb://mongo:27017/school_db
PORT=5000
JWT_SECRET=your_secret_key
```

---

### ⚡ Step 3: Build and Run with Docker Compose

```bash
docker-compose up --build
```

This command will:
- Build images for frontend, backend, and MongoDB
- Create a local Docker network
- Run all containers together

---

### ⚡ Step 4: Access the Application

Once containers are running:
- 🌐 Frontend: [http://localhost:3000](http://localhost:3000)
- ⚙️ Backend API: [http://localhost:5000](http://localhost:5000)
- 🗄 MongoDB: accessible internally via `mongo:27017`

To stop the containers:
```bash
docker-compose down
```

---

## 🧱 CI/CD Pipeline (Jenkins)

The `Jenkinsfile` automates your complete CI/CD workflow:

```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ebadarshad/mern-school-management"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ebad-arshad/MERN-School-Management-System.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'npm install --prefix backend && npm test --prefix backend'
            }
        }

        stage('Docker Build & Push') {
            steps {
                sh '''
                docker build -t $DOCKER_IMAGE:$BUILD_NUMBER .
                docker login -u $DOCKER_USER -p $DOCKER_PASS
                docker push $DOCKER_IMAGE:$BUILD_NUMBER
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f k8s/
                kubectl rollout status deployment/backend
                '''
            }
        }
    }
}
```

✅ Automatically triggers when you push to GitHub  
✅ Builds, tests, and pushes Docker images to Docker Hub  
✅ Deploys the latest version to Kubernetes  

---

## ☸️ Kubernetes Deployment

The project includes a complete Kubernetes setup under `/k8s`:

- `deployment.yaml` — Deploys backend, frontend, MongoDB
- `service.yaml` — Exposes the app internally
- `ingress.yaml` — Routes external traffic
- `hpa.yaml` — Enables autoscaling based on CPU usage
- `mongo-pv.yaml` — Persistent volume for MongoDB data

### Run on Minikube

```bash
minikube start
kubectl apply -f k8s/
minikube service frontend-service
```

---

## 🧠 Future Enhancements

- Integrate **Prometheus & Grafana** for observability  
- Add **Helm charts** for simplified K8s management  
- Add **Trivy** for image vulnerability scanning  
- Use **ArgoCD** or **GitHub Actions** for GitOps automation  

---

## 👨‍💻 Author

**Ebad Arshad**  
📍 DevOps Engineer | Docker | Jenkins | Kubernetes | CI/CD  
🔗 [GitHub Profile](https://github.com/ebad-arshad)  
📫 Connect on [LinkedIn](https://linkedin.com/in/ebadarshad)

---

### 💡 If this project helped you learn something, give it a ⭐ on GitHub!
