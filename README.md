# 🚀 Kubernetes Demo App – Notes Profile Web Application

This project demonstrates a complete Kubernetes-based deployment of a simple web application with a MongoDB backend. It showcases how to deploy, configure, and expose a multi-tier application using Kubernetes best practices.

---

## 📌 Project Overview

The application allows users to:

* View a profile (name, email, interests)
* Update profile data
* Store and retrieve data from MongoDB

The project focuses on **infrastructure and deployment**, not just the application logic.

---

## 🏗️ Architecture

The system consists of:

* **Web Application (Node.js)**
  Handles HTTP requests and serves the frontend UI

* **MongoDB Database**
  Stores user profile data

* **Kubernetes Components**

  * Deployment (App & MongoDB)
  * Service (ClusterIP & NodePort)
  * ConfigMap (non-sensitive config)
  * Secret (credentials)

```
User → Webapp Service → Webapp Pod → Mongo Service → Mongo Pod
```

---

## ⚙️ Technologies Used

* Kubernetes (Minikube for local cluster)
* Docker
* Node.js (Express)
* MongoDB
* kubectl

---

## 📁 Project Structure

```
.
├── webapp-deployment.yaml
├── webapp-service.yaml
├── mongo-deployment.yaml
├── mongo-service.yaml
├── mongo-config.yaml
├── mongo-secret.yaml
└── README.md
```

---

## 🔐 Configuration

### ConfigMap

Used for non-sensitive data like database URL:

```yaml
mongo-url: mongo-service
```

### Secret

Used for sensitive credentials:

```yaml
mongo-user: mongouser
mongo-password: mongopassword
```

---

## 🚀 How to Run the Project

### 1. Start Minikube

```bash
minikube start
```

---

### 2. Apply Kubernetes Resources

```bash
kubectl apply -f .
```

---

### 3. Verify Pods

```bash
kubectl get pods
```

Ensure all pods are in `Running` state.

---

### 4. Access the Application

#### Option A (Recommended for macOS)

```bash
kubectl port-forward service/webapp-service 3000:3000
```

Then open:

```
http://localhost:3000
```

---

#### Option B (NodePort)

```bash
minikube ip
```

Then:

```
http://<MINIKUBE_IP>:30100
```

---

## 🧪 Debugging Tips

### Check Pods

```bash
kubectl get pods
```

### View Logs

```bash
kubectl logs deployment/webapp-deployment
```

### Describe Resource

```bash
kubectl describe pod <pod-name>
```

### Test API

```bash
curl http://localhost:3000/get-profile
```

---

## ⚠️ Common Issues & Fixes

### 1. White Page in Browser

* Cause: `/get-profile` API failing
* Fix: Check logs and Mongo connection

---

### 2. Secret Misconfiguration

* Ensure correct usage of `stringData` vs `data`
* Ensure correct key names

---

### 3. Service Not Reachable

* Verify NodePort or use `port-forward`
* Ensure selector matches pod labels

---

### 4. Mongo Connection Issues

* Ensure ConfigMap and Secret values are correct
* Restart deployments after changes:

```bash
kubectl rollout restart deployment webapp-deployment
```

---

## 🔄 Useful Commands

```bash
kubectl apply -f .
kubectl delete -f .
kubectl get all
kubectl rollout restart deployment webapp-deployment
```

---

## 📈 Future Improvements

* Add Ingress with domain routing
* Implement liveness & readiness probes
* Use Persistent Volumes for MongoDB
* Add CI/CD pipeline (GitHub Actions)
* Deploy to cloud (AWS EKS / GKE)

---

## 🧠 What This Project Demonstrates

* Kubernetes fundamentals (Deployments, Services, ConfigMaps, Secrets)
* Real-world debugging workflow
* Multi-service application architecture
* Environment configuration management
* Service exposure and networking

---

## 👤 Author

**Ameer Adel**
Aspiring DevOps Engineer 🚀

---

## ⭐ Final Notes

This project is built for learning and demonstrating practical DevOps skills.
It simulates real-world deployment and troubleshooting scenarios using Kubernetes.

---
