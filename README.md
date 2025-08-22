# 🚀 HRMS Deployment on Kubernetes with CI/CD & Monitoring

This project demonstrates the deployment of a **3-Tier HRMS Application** (Frontend, Backend, MySQL Database) using **Docker, Kubernetes (kubeadm cluster), Jenkins CI/CD pipeline, and Monitoring with Prometheus & Grafana**.

It is designed as a **DevOps Portfolio Project** to showcase:
- Containerization with Docker  
- Orchestration with Kubernetes  
- Continuous Integration & Continuous Delivery (CI/CD) using Jenkins  
- Monitoring & Observability using Prometheus + Grafana  
- Best practices for Secrets, ConfigMaps, StatefulSets, and Ingress  

## 🏗️ Project Architecture

```mermaid
flowchart LR
    A[Developer] --> B[GitHub Repo]
    B --> C[Jenkins Pipeline]
    C --> D[Docker Hub]
    D --> E["Kubernetes Cluster - kubeadm"]
    E --> F[Frontend Service]
    E --> G[Backend Service]
    E --> H[(MySQL StatefulSet)]
    E --> I[Prometheus]
    I --> J[Grafana Dashboards]
