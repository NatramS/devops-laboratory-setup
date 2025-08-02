# devops-laboratory-setup
This repository has the instructions on how to setup DevOps lab and integrate the tools and applications

Overview

This project demonstrates a complete DevOps lab setup that builds, analyzes, stores, and deploys a Java application using:

Jenkins (Master + Slave) – CI/CD automation
SonarQube – Code quality analysis
Nexus Repository – Artifact storage
Kubernetes (K8s) – Deployment of application
OWASP Dependency Check – Security vulnerability scanning
Aqua Trivy – Docker image scanning

Architecture

                ┌──────────┐
                │ Developer│
                └────┬─────┘
                     │ Git Push
                     ▼
          ┌──────────────────────┐
          │ Jenkins Master + Slave│
          └──────┬─────────┬─────┘
                 │         │
                 ▼         ▼
       ┌────────────────┐ ┌──────────────────┐
       │ SonarQube       │ │ OWASP/Trivy Scan │
       └────────────────┘ └──────────────────┘
                 │
                 ▼
       ┌────────────────┐
       │ Nexus Repository│
       └────────────────┘
                 │
                 ▼
       ┌────────────────┐
       │ Kubernetes      │
       │ (Master + 2     │
       │ Workers)        │
       └────────────────┘

Requirements

| Component         | Count | Purpose               |
| ----------------- | ----- | --------------------- |
| Jenkins Master    | 1     | CI/CD orchestration   |
| Jenkins Slave     | 1     | Build execution       |
| SonarQube         | 1     | Code quality analysis |
| Nexus             | 1     | Artifact repository   |
| Kubernetes Master | 1     | K8s control plane     |
| Kubernetes Worker | 2     | App hosting           |


Tools & Technologies

AWS EC2 – Hosting VMs
Ubuntu 22.04 LTS – OS
Java 17 – Required for Jenkins
Docker – SonarQube, Nexus, Jenkins agents
Maven – Build tool
Terraform / Ansible (Optional) – Automation
kubectl, kubeadm, kubelet – Kubernetes management


Setup Steps

1️⃣ Provision Infrastructure
Create EC2 instances for Jenkins, SonarQube, Nexus, and Kubernetes nodes.
Configure Security Groups to open:
Jenkins: 8080
SonarQube: 9000
Nexus: 8081
K8s API: 6443
Node Ports: 30000-32767

2️⃣ Install & Configure Jenkins
Install Java 17

3️⃣ Install & Configure SonarQube
Installation and setup of Docker

4️⃣ Install & Configure Nexus
Install Docker & run Nexus

5️⃣ Connect Jenkins with SonarQube & Nexus
Create tokens in SonarQube & Nexus

6️⃣ Jenkins Pipeline
Pipeline stages:
Git Checkout – Fetch source code.
OWASP Dependency Check – Security scan.
SonarQube Analysis – Code quality check.
Build with Maven – Package .jar or .war.
Upload Artifact to Nexus.
Deploy to Kubernetes.

7️⃣ Kubernetes Setup

📦 Final Outcome
Code is pulled from GitHub → scanned → built → stored in Nexus → deployed on Kubernetes → accessible via LoadBalancer/NodePort.
