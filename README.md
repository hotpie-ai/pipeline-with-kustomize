# Kubernetes Pipeline with Git & Jenkins

> **Project:** `pipeline-with-kustomize`

This project demonstrates a simple CI/CD pipeline to deploy a Kubernetes application using GitHub, Jenkins, and Kustomize. It is intended to help others quickly get started with automated deployment pipelines on Kubernetes clusters.

---

## 🚀 What You'll Learn

- Creating a Kubernetes deployment pipeline  
- Using GitHub as the source of truth  
- Automating deployments with Jenkins  
- Managing Kubernetes resources with Kustomize  

---

## 🧰 Tech Stack

- **GitHub** – Source code repository  
- **Jenkins** – CI/CD automation  
- **Kubernetes** – Deployment platform  
- **Kustomize** – YAML templating and customization  

---

## 📝 Prerequisites

- Jenkins installed and running (local or remote)  
- Access to a Kubernetes cluster  
- `kubectl` and `kustomize` installed on the Jenkins node (or controller)  
- A GitHub account with a repository containing your Kubernetes manifests  

---

## 🧪 Example: NGINX Deployment

We'll deploy an NGINX container to the Kubernetes cluster using Kustomize.
---
### 📁 Project Structure

```bash
pipeline-with-kustomize/
├── base/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
├── overlays/
│   └── dev/
│       ├── kustomization.yaml
│       └── replica-patch.yaml
└── Jenkinsfile
```
## 🧩 base/deployment.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```
## 🧩 base/service.yaml
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```
## 🧩 base/kustomization.yaml
```
resources:
  - deployment.yaml
  - service.yaml
```
## 🧩 overlays/dev/kustomization.yaml
```
resources:
  - ../../base
patchesStrategicMerge:
  - replica-patch.yaml
```
## 🧩 overlays/dev/replica-patch.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 2
```
## 🧩 Jenkinsfile
```
pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/yourusername/pipeline-with-kustomize.git'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -k overlays/dev/'
            }
        }
    }
}
```

