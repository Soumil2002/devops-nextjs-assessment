# DevOps Internship Assessment: Containerize and Deploy a Next.js Application

## **Project Overview**

This project demonstrates how to:

- Containerize a Next.js application using Docker  
- Automate Docker build and push using GitHub Actions and GitHub Container Registry (GHCR)  
- Deploy the containerized app to Kubernetes (Minikube)  
- Access the deployed application  

---

## **Table of Contents**

1. [Project Setup](#project-setup)  
2. [Dockerization](#dockerization)  
3. [GitHub Actions Workflow](#github-actions-workflow)  
4. [Kubernetes Deployment](#kubernetes-deployment)  
5. [Accessing the Application](#accessing-the-application)  
6. [Repository & GHCR Links](#repository--ghcr-links)  

---

## **Project Setup**

### 1. Clone the Repository

```bash
git clone https://github.com/Soumil2002/devops-nextjs-assessment.git
cd devops-nextjs-assessment
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Run Locally

```bash
npm run dev
```

- Open browser: [http://localhost:3000](http://localhost:3000)  

<img width="2544" height="1364" alt="Screenshot 2025-10-06 at 15 16 26" src="https://github.com/user-attachments/assets/dccf6858-75e9-4ffa-b26e-cd2cf0d13676" />

---

## **Dockerization**

### 1. Build Docker Image

```bash
docker build -t ghcr.io/soumil2002/devops-nextjs-app:latest .
```

### 2. Run Docker Container Locally

```bash
docker run -p 3000:3000 ghcr.io/soumil2002/devops-nextjs-app:latest
```

- Open browser: [http://localhost:3000](http://localhost:3000)  


---

## **GitHub Actions Workflow**

- Workflow file: `.github/workflows/docker-publish.yml`  
- This workflow builds the Docker image and pushes it to GHCR automatically on every push to the `main` branch.  
- Make sure your **GHCR personal access token (PAT)** is added in GitHub Secrets as `GHCR_PAT`.  

---

<img width="2552" height="1296" alt="Screenshot 2025-10-06 at 15 14 18" src="https://github.com/user-attachments/assets/0fcca639-c007-49f2-9f63-efe16cbebcf0" />

<img width="2544" height="1064" alt="Screenshot 2025-10-06 at 15 14 36" src="https://github.com/user-attachments/assets/c20e214e-fb94-4bbc-8049-accdb99c73f6" />


## **Kubernetes Deployment**

> Note: Deployment and service manifests are already present in `k8s/` folder (`deployment.yaml` and `service.yaml`).  

### 1. Start Minikube

```bash
minikube start
```

### 2. Apply Kubernetes Manifests

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### 3. Verify Pods & Service

```bash
kubectl get pods
kubectl get svc
```

---

## **Accessing the Application**

### Option 1: Using Minikube Service Command

```bash
minikube service devops-nextjs-service
```

- Opens the app in your default browser automatically  

### Option 2: Using NodePort Manually

1. Get Minikube IP:

```bash
minikube ip
```

2. Get NodePort:

```bash
kubectl get svc devops-nextjs-service
```

3. Open browser:

```
http://<minikube-ip>:<NodePort>
```

> Example: `http://192.168.49.2:30379`  

---

## **Repository & GHCR Links**

- GitHub Repository: [https://github.com/Soumil2002/devops-nextjs-assessment](https://github.com/Soumil2002/devops-nextjs-assessment)  
- GHCR Docker Image: `ghcr.io/soumil2002/devops-nextjs-app:latest`  

---

## **Notes**

- Docker image is **public**, so Kubernetes can pull it without authentication  
- Readiness and liveness probes ensure pods restart if unhealthy  
- Minikube NodePort exposes the app for local testing  
- GitHub Actions automates Docker image build and push

