🗳️ Cloud-Native Voting Application
Kubernetes + CI/CD on AWS EKS










A cloud-native microservices application deployed on AWS EKS with NGINX Ingress, Cloudflare DNS, and a fully automated GitHub Actions CI/CD pipeline.

This project demonstrates the evolution from manual Kubernetes deployments to a production-ready automated DevOps workflow.

🚀 Live Architecture Overview
User
 │
 ▼
Cloudflare DNS
 │
 ▼
AWS Load Balancer (ELB)
 │
 ▼
NGINX Ingress Controller
 │
 ▼
Kubernetes Services
🏗️ System Architecture
                    🌍 Internet
                         │
                         ▼
                Cloudflare DNS
                         │
                         ▼
              AWS ELB (LoadBalancer)
                         │
                         ▼
              NGINX Ingress Controller
                         │
     ┌──────────────────────────────────┐
     │           EKS Cluster            │
     │                                  │
     │  🐍 Vote Service (Python Flask)  │
     │  🌐 Result Service (Node.js)     │
     │  ⚙️ Worker (.NET Core)           │
     │  🧠 Redis Queue                  │
     │  🐘 PostgreSQL Database          │
     │                                  │
     └──────────────────────────────────┘
🧩 Microservices
Service	Technology	Purpose
🐍 Vote	Python Flask	Collects votes
🌐 Result	Node.js	Displays voting results
⚙️ Worker	.NET Core	Processes queued votes
🧠 Redis	In-memory queue	Message broker
🐘 PostgreSQL	Database	Stores results
🧱 Tech Stack
Cloud Infrastructure

AWS EKS

AWS Load Balancer

Cloudflare DNS

Containerization

Docker

Docker Hub

Orchestration

Kubernetes

NGINX Ingress Controller

CI/CD

GitHub Actions

Security

Kubernetes Secrets

ConfigMaps

⚙️ Deployment Evolution

This project demonstrates two deployment approaches.

1️⃣ Manual Kubernetes Deployment

Initial deployments were executed manually.

Deployment Workflow
Build Docker Image
        │
        ▼
Push to Docker Hub
        │
        ▼
kubectl apply -f k8s/
        │
        ▼
Application deployed to EKS
Components Used

Kubernetes Deployments

Kubernetes Services

ConfigMaps

Secrets

NGINX Ingress

2️⃣ Automated CI/CD Deployment

The project was upgraded with a fully automated GitHub Actions pipeline.

CI/CD Pipeline
Developer Push
      │
      ▼
GitHub Actions Triggered
      │
      ▼
Build Docker Images
(vote, result, worker)
      │
      ▼
Push Images → Docker Hub
      │
      ▼
Inject GitHub Secrets
      │
      ▼
Deploy to AWS EKS
      │
      ▼
Rolling Update via Kubernetes
⚡ CI/CD Benefits

🚀 Zero manual deployments

🔐 Secure secret handling

⚡ Faster production releases

📉 Reduced configuration drift

♻️ Immutable container deployments

🌐 DNS & Routing

DNS is managed via Cloudflare.

Traffic flow:

User → Cloudflare → AWS ELB → NGINX Ingress → Kubernetes Services
Host Routing
Domain	Service
vote.domain.com	Vote service
result.domain.com	Result service
🔐 Secret Management

Sensitive data is never committed to GitHub.

Secrets are handled through:

GitHub Secrets

Kubernetes Secrets

Runtime environment injection

Example secrets:

Database credentials

Redis connection strings

Application configuration

📁 Project Structure
.
├── k8s/
│   ├── namespace.yaml
│   ├── postgres.yaml
│   ├── redis.yaml
│   ├── vote.yaml
│   ├── result.yaml
│   ├── worker.yaml
│   └── ingress.yaml
│
├── vote/
├── result/
├── worker/
│
└── .github/
    └── workflows/
        └── cicd.yml
⚠️ Challenges Faced

This project required deep debugging across networking, DNS, and Kubernetes layers.

Key Issues Solved

🌍 A Record vs CNAME confusion

🔁 Cloudflare proxy vs DNS-only conflicts

🚫 404 errors from incorrect Ingress host rules

🔐 Secure secret injection

⚙️ Worker connection failures due to environment mismatch

Debugging Tools Used
kubectl logs
kubectl describe
kubectl get ingress
kubectl get svc
curl -H "Host:..."
📚 Engineering Lessons Learned

Kubernetes routing is host-header driven

Ingress 404 errors often indicate routing issues

CI/CD eliminates operational deployment overhead

Secrets should never be version controlled

Automation drastically reduces human error

Observability is essential for debugging distributed systems

🎯 What This Project Demonstrates

✅ Multi-language microservices architecture
✅ Containerized application deployment
✅ Kubernetes service discovery
✅ Ingress-based routing
✅ Production-style DNS configuration
✅ Secure secret management
✅ Automated CI/CD pipelines
✅ Real-world DevOps troubleshooting

🔮 Future Improvements

🔐 cert-manager for automatic TLS certificates

📊 Prometheus + Grafana monitoring

🧪 Automated integration tests in CI

📦 Helm packaging

🔄 Blue/Green deployments

👨‍💻 Author

Prince Onuoha

DevOps Engineer focused on cloud-native infrastructure, Kubernetes, and automated deployment pipelines.
