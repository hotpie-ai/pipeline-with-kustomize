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
