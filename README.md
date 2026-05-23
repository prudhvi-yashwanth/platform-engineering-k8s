# Cloud-Native CI/CD & Kubernetes Platform Engineering Project

A production-style cloud-native platform engineering project built using Kubernetes, GitHub Actions, Docker, and DevSecOps tooling.

This project demonstrates end-to-end CI/CD automation, Kubernetes deployment workflows, security scanning, autoscaling, rolling deployments, and high availability concepts using a local Kubernetes environment powered by k3d.

---

# Architecture Overview

<img width="1536" height="1024" alt="k8s-platform-arc" src="https://github.com/user-attachments/assets/507c9b5a-022d-4c9d-8cdf-0ed17c6ffa1c" />

---

# Project Goals

The primary objective of this project was to design and implement a modern cloud-native deployment platform with:

- CI/CD automation
- Kubernetes-based deployments
- Secure software delivery
- Deployment self-healing
- High availability
- Autoscaling
- DevSecOps practices

The project was intentionally designed in a modular and production-oriented manner to simulate real-world platform engineering workflows.

---

# Tech Stack

| Category | Tools & Technologies |
|---|---|
| Programming Language | Go |
| Containerization | Docker |
| Kubernetes | k3d + kubectl |
| CI/CD | GitHub Actions |
| Ingress | NGINX Ingress Controller |
| Security Scanning | Trivy |
| Secret Scanning | Gitleaks |
| Scaling | Kubernetes HPA |
| High Availability | PodDisruptionBudget |
| Version Control | Git + GitHub |

---

# Features Implemented

## CI Pipeline
- Source code checkout
- Go build validation
- Unit testing
- Docker image build
- Trivy vulnerability scanning
- Gitleaks secret scanning

## CD Pipeline
- Automated deployment after CI success
- Kubernetes rollout verification
- Dynamic image deployment using Git commit SHA

## Kubernetes Features
- Kubernetes Deployments
- ClusterIP Services
- NGINX Ingress Controller
- Liveness Probes
- Readiness Probes
- Rolling Updates
- Horizontal Pod Autoscaler (HPA)
- PodDisruptionBudget (PDB)

## Security
- Vulnerability scanning using Trivy
- Secret leak detection using Gitleaks
- Non-root container execution
- Kubernetes security best practices

---

# Repository Structure

```bash
platform-engineering-k8s/
├── app
│   ├── cmd
│   │   └── api
│   │       ├── main.go
│   │       └── main_test.go
│   ├── Dockerfile
│   └── go.mod
│
├── k8s
│   ├── base
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   ├── hpa.yaml
│   │   └── pdb.yaml
│   │
│   └── ingress
│       └── ingress.yaml
│
├── .github
│   └── workflows
│       ├── ci.yaml
│       └── cd.yaml
│
├── docs
│
├── scripts
│
└── README.md
```

---

# CI/CD Workflow

```text
Developer
   ↓
Git Push
   ↓
Pull Request Validation
   ↓
CI Pipeline
   ├── Build
   ├── Test
   ├── Docker Build
   ├── Trivy Scan
   └── Gitleaks Scan
         ↓
Merge to develop
         ↓
CD Pipeline
         ↓
Deploy to Kubernetes
         ↓
Rolling Update
         ↓
HPA & High Availability
```

---

# Kubernetes Self-Healing

The platform uses Kubernetes reconciliation mechanisms to maintain desired state automatically.

Implemented self-healing capabilities:
- Pod recreation after failure
- Health probe based recovery
- Replica reconciliation
- Rolling deployments
- Autoscaling through HPA

---

# Security & DevSecOps

## Trivy
Container image vulnerability scanning integrated directly into CI pipeline.

Checks:
- HIGH vulnerabilities
- CRITICAL vulnerabilities

## Gitleaks
Repository secret scanning integrated into CI pipeline.

Checks:
- API keys
- Tokens
- Credentials
- Secret leaks in commit history

---

# Local Environment Setup

## Prerequisites

Install the following:

- Docker Desktop
- kubectl
- k3d
- Helm
- Git
- Go
- Trivy
- Gitleaks

---

# Create Kubernetes Cluster

```bash
k3d cluster create dev-platform
```

---

# Deploy Application

```bash
kubectl apply -f k8s/base/
kubectl apply -f k8s/ingress/
```

---

# Verify Deployment

```bash
kubectl get pods -n dev
```

```bash
kubectl get hpa -n dev
```

```bash
kubectl get pdb -n dev
```

---

# Access Application

```bash
curl http://api.localdev.me
```

---

# CI/CD Highlights

## Branch Strategy

| Branch | Purpose |
|---|---|
| develop | Active deployment branch |
| feature/* | Feature development |

## Workflow Behavior

- Pull Requests trigger CI validation only
- Merge to `develop` triggers CI + CD deployment

---

# Future Improvements

Planned AWS migration project:
- Terraform infrastructure provisioning
- Amazon EKS
- IAM & IRSA
- AWS ALB Controller
- Route53
- Prometheus & Grafana
- ArgoCD GitOps
- Cloud-native observability stack
- Infrastructure drift detection & remediation

---

# Key Learnings

This project provided hands-on experience with:

- Kubernetes reconciliation patterns
- CI/CD orchestration
- Self-hosted GitHub Actions runners
- DevSecOps integration
- Deployment automation
- Cloud-native deployment strategies
- Kubernetes scaling and availability concepts

---

# Author

Prudhvi Yashwanth Reddy Kikkuru

DevOps Engineer | Kubernetes | Cloud-Native | CI/CD | Platform Engineering

---

# License

This project is for learning, demonstration, and portfolio purposes.
