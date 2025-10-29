# 🚀 MERN School Management System – CI/CD with Jenkins & ArgoCD

## 📘 Overview

This project demonstrates a **complete CI/CD pipeline** implementation for a **MERN (MongoDB, Express, React, Node.js)** School Management System — from containerization to deployment in a Kubernetes cluster, fully automated with **Jenkins** and **ArgoCD** following **GitOps principles**.

The system includes:
- 🖥️ Frontend (React)
- ⚙️ Backend (Node.js, Express)
- 🗄️ MongoDB (StatefulSet)

This project was designed and built **from scratch after the code part** as part of a hands-on DevOps learning journey — implementing industry-grade automation using open-source tools.

---

## 🧩 Tech Stack

| Category | Tool |
|-----------|------|
| Containerization | **Docker** |
| Orchestration | **Kubernetes (Minikube)** |
| CI/CD | **Jenkins + ArgoCD (GitOps)** |
| Image Registry | **Docker Hub** |
| Secret Management | **Kubernetes Secrets** |
| Version Control | **GitHub** |

---

## ⚙️ Architecture Flow

```
 Developer Push Code ─────┐
                          ▼
                   Jenkins (CI)
                 ├─ Build & Test
                 ├─ Trivy Security Scan
                 ├─ Build Docker Image
                 ├─ Push to Docker Hub
                 └─ Update GitHub K8s Manifests
                          │
                          ▼
                     GitHub Repo
                          │
                          ▼
                   ArgoCD (CD - GitOps)
                 ├─ Watches Repo
                 ├─ Syncs Deployment
                 └─ Applies to Cluster
                          │
                          ▼
               Kubernetes Cluster (Minikube)
                 ├─ MongoDB StatefulSet
                 ├─ Frontend Deployment
                 └─ Backend Deployment
```

---

## 🧱 Project Components

| Component | Description |
|------------|-------------|
| **Dockerfiles** | Containerization for frontend & backend |
| **Kubernetes YAMLs** | Deployments, Services, StatefulSets, Secrets |
| **Jenkinsfile** | Pipeline as code for CI automation |
| **ArgoCD Application** | Continuous delivery setup |
| **Secrets Management** | Kubernetes Secrets |

---

## 🧰 Jenkins Pipeline (CI)

Stages:
1. **Checkout Code** – Pull from GitHub  
2. **Build Docker Images** – Tag images with `${BUILD_NUMBER}`  
3. **Trivy Scan** – Check for vulnerabilities  
4. **Push to DockerHub** – Upload new image versions  
5. **Update K8s YAMLs** – Change image tag in deployment manifests  
6. **Push to GitHub** – Trigger ArgoCD for delivery  

---

## 🚀 ArgoCD (CD - GitOps)

- Deployed inside Kubernetes  
- Configured to watch this repository branch k8s of (`k8s/` folder)
- Syncs changes automatically from GitHub to the cluster  
- Uses **sync waves** to apply resources in order:
  ```
  0 - Namespace
  1 - PV
  2 - PVC
  3 - Secrets
  4 - Services
  5 - StatefulSet (Mongo)
  6 - Deployments (Frontend/Backend)
  7 - HPA
  ```

---

## 🧠 Key Learnings

✅ Dockerized full-stack MERN app  
✅ Built and managed Kubernetes objects manually  
✅ Created CI pipeline in Jenkins using declarative syntax  
✅ Implemented GitOps delivery through ArgoCD  
✅ Managed resource sync dependencies using Argo sync waves  
✅ Learned troubleshooting of pods, PVCs, and certificates  
✅ Automated full pipeline — **Code → Image → Deploy**

---

## 🧑‍💻 Author

**👋 Muhammad Ebad Arshad**  
🚀 DevOps Engineer (in progress) | Linux | Docker | Kubernetes | Jenkins | ArgoCD | GitOps | Cloud Learner  
🔗 [LinkedIn](https://linkedin.com/in/ebad-arshad) | [GitHub](https://github.com/ebad-arshad)
