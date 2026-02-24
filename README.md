🗳️ Cloud-Native Voting Application
Kubernetes + CI/CD on AWS EKS

A fully containerized microservices application deployed on AWS EKS with NGINX Ingress, Cloudflare DNS, and a complete GitHub Actions CI/CD pipeline.

This project demonstrates the evolution from manual Kubernetes deployments to a production-ready automated DevOps workflow.

🚀 Live Architecture Overview

🌍 User → Cloudflare DNS → AWS Load Balancer → NGINX Ingress → Kubernetes Services

Microservices:

🐍 Vote – Python (Flask)

🌐 Result – Node.js

⚙️ Worker – .NET Core

🧠 Redis – Queue

🐘 PostgreSQL – Database

🏗️ Architecture Diagram
Internet
   │
Cloudflare DNS
   │
AWS ELB (LoadBalancer)
   │
NGINX Ingress Controller
   │
┌─────────────────────────────┐
│         EKS Cluster         │
│                             │
│  Vote (Python)              │
│  Result (Node)              │
│  Worker (.NET)              │
│  Redis                      │
│  PostgreSQL                 │
└─────────────────────────────┘
🧩 Tech Stack

☁️ AWS EKS

🐳 Docker

☸️ Kubernetes

🔀 NGINX Ingress

🌍 Cloudflare DNS

🔐 Kubernetes Secrets & ConfigMaps

🔄 GitHub Actions CI/CD

🧱 Infrastructure as Code mindset

🛠️ Deployment Methods
1️⃣ Manual Kubernetes Deployment

Initial deployment was done using:

Docker image builds

Docker Hub push

kubectl apply -f k8s/

ConfigMaps & Secrets for environment configuration

Ingress for routing traffic

Manual Flow:
Build Docker Image
    ↓
Push to Docker Hub
    ↓
kubectl apply
    ↓
Application Live
2️⃣ Automated CI/CD Deployment (GitHub Actions)

The project was enhanced with a fully automated CI/CD pipeline.

Pipeline Stages:

📦 Code pushed to GitHub

🐳 Build Docker images (vote, result, worker)

📤 Push images to Docker Hub

🔐 Inject secrets securely from GitHub Secrets

☸️ Deploy to EKS automatically

🔁 Rolling update of services

CI/CD Benefits:

🚀 Zero manual deployments

🔐 Secure secret handling

📉 Reduced configuration drift

⚡ Faster production updates

♻️ Immutable deployments

🌐 DNS & Routing

Domain managed via Cloudflare

CNAME records point to AWS ELB

NGINX Ingress handles host-based routing

Example:

vote.domain.com → Vote service

result.domain.com → Result service

🔐 Secret Management

Sensitive values are not committed to GitHub.

Instead:

Kubernetes Secrets are generated dynamically

GitHub Secrets are used during CI/CD

Secure environment injection at deployment time

📁 Project Structure
.
├── k8s/
│   ├── namespace.yaml
│   ├── postgres.yaml
│   ├── redis.yaml
│   ├── vote.yaml
│   ├── result.yaml
│   ├── worker.yaml
│   ├── ingress.yaml
│
├── vote/
├── result/
├── worker/
│
└── .github/workflows/
    └── cicd.yml
⚠️ Challenges Faced

This project required deep debugging across networking, DNS, and Kubernetes layers.

Key Challenges:

🔄 A Record vs CNAME confusion (ELB hostname routing)

🌍 Cloudflare proxy vs DNS-only conflicts

🚫 404 errors due to incorrect Ingress host matching

🔐 Secure secret handling without exposing credentials

🧩 Worker failing to connect due to environment mismatch

🧠 Debugging using:

kubectl logs

kubectl describe

kubectl get ingress

curl -H "Host:..."

📚 Engineering Lessons Learned

Kubernetes networking is host-header driven

Ingress 404 ≠ app failure (routing mismatch)

CI/CD eliminates operational overhead

Secrets should never be version controlled

Automation reduces human deployment error

Observability is critical for debugging distributed systems

🎯 What This Project Demonstrates

✅ Containerization of multi-language microservices
✅ Kubernetes service discovery
✅ Ingress-based routing
✅ Production-style DNS setup
✅ Secure secret management
✅ End-to-end CI/CD automation
✅ Real-world DevOps troubleshooting

🧠 Future Improvements

🔐 cert-manager for automatic TLS certificates

📊 Prometheus + Grafana monitoring

🧪 Automated integration testing in CI

📦 Helm packaging

🔄 Blue/Green deployments

👨‍💻 Author

Built as part of a DevOps engineering project demonstrating cloud-native architecture, automation, and production deployment practices.
