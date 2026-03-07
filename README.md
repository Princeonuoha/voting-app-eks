## 🏗️ Kubernetes Architecture

```mermaid
flowchart TD

User[🌍 User] --> Cloudflare[Cloudflare DNS]

Cloudflare --> ELB[AWS Load Balancer]

ELB --> Ingress[NGINX Ingress Controller]

Ingress --> Vote[Vote Service<br>Python Flask]

Ingress --> Result[Result Service<br>Node.js]

Vote --> Redis[Redis Queue]

Redis --> Worker[Worker Service<br>.NET Core]

Worker --> Postgres[PostgreSQL Database]

Result --> Postgres

User → Cloudflare DNS → AWS Load Balancer → NGINX Ingress → Kubernetes Services

⚙️ Microservices Architecture

| Service       | Technology      | Purpose                |
| ------------- | --------------- | ---------------------- |
| 🐍 Vote       | Python Flask    | Collects votes         |
| 🌐 Result     | Node.js         | Displays results       |
| ⚙️ Worker     | .NET Core       | Processes queued votes |
| 🧠 Redis      | In-memory queue | Message broker         |
| 🐘 PostgreSQL | Database        | Stores results         |

🔄 CI/CD Pipeline

Pipeline Flow

Developer Push
      ↓
GitHub Actions Triggered
      ↓
Build Docker Images
      ↓
Push Images to Docker Hub
      ↓
Deploy to AWS EKS
      ↓
Rolling Update
🎥 Live Application Demo

The demo shows:

Submitting a vote

Processing via Redis queue

Worker storing results in PostgreSQL

Result service displaying updated data

🧩 Tech Stack
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

🚀 Deployment Methods
1️⃣ Manual Kubernetes Deployment

Initial deployment used manual Kubernetes operations.

Build Docker Image
      ↓
Push to Docker Hub
      ↓
kubectl apply -f k8s/
      ↓
Application Live

Resources used

Deployments

Services

ConfigMaps

Secrets

Ingress Controller

2️⃣ Automated CI/CD Deployment

The project was later upgraded with GitHub Actions automation.

Code Push → GitHub Actions → Build Images → Push to Docker Hub → Deploy to EKS
Benefits

🚀 Zero manual deployments

🔐 Secure secret handling

⚡ Faster releases

📉 Reduced configuration drift

♻️ Immutable deployments

🌐 DNS & Routing

DNS is managed via Cloudflare.

Routing example:

Domain	Service
vote.domain.com	Vote service
result.domain.com	Result service

Traffic routing:

User → Cloudflare → AWS ELB → NGINX Ingress → Kubernetes Pods
🔐 Secret Management

Sensitive configuration is never committed to GitHub.

Secrets are injected via:

GitHub Secrets

Kubernetes Secrets

Runtime environment variables

Examples:

Database credentials

Redis connection strings

API configuration

📁 Project Structure
.
├── k8s
│   ├── namespace.yaml
│   ├── postgres.yaml
│   ├── redis.yaml
│   ├── vote.yaml
│   ├── result.yaml
│   ├── worker.yaml
│   └── ingress.yaml
│
├── vote
├── result
├── worker
│
├── docs
│   ├── architecture.png
│   ├── pipeline.png
│   └── demo.gif
│
└── .github
    └── workflows
        └── cicd.yml
⚠️ Challenges Faced

This project required debugging across networking, DNS, and Kubernetes layers.

Key issues solved:

🌍 A record vs CNAME confusion

🌐 Cloudflare proxy conflicts

🚫 Ingress host mismatch causing 404 errors

🔐 Secure secret injection

⚙️ Worker service environment mismatch

Debugging tools used

kubectl logs
kubectl describe
kubectl get ingress
kubectl get svc
curl -H "Host:..."
📚 Engineering Lessons Learned

Kubernetes routing is host-header driven

Ingress 404 errors often indicate routing issues

CI/CD drastically reduces operational overhead

Secrets should never be version controlled

Observability is critical for debugging distributed systems

🔮 Future Improvements

cert-manager for automatic TLS

Prometheus + Grafana monitoring

Helm packaging

Integration tests in CI

Blue/Green deployments

👨‍💻 Author

Prince Onuoha

DevOps Engineer focused on cloud-native infrastructure, Kubernetes, and automated deployment pipelines.


