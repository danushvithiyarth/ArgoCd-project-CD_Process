# 🚀 ArgoCD Project – CD Pipeline

**Purpose:** This repository handles **Continuous Deployment (CD)** using **GitOps methodology with ArgoCD**.  
It automatically deploys containerized applications to Kubernetes (AWS EKS) and integrates monitoring, ingress, and DNS management.

Application source code built in the CI repository: [Boardgame](https://github.com/jaiswaladi246/Boardgame.git)

---

## 🧰 Technologies & Tools

| Category | Tools |
|----------|-------|
| Kubernetes | AWS EKS, kubectl |
| GitOps | ArgoCD |
| Deployment | Helm, Kubernetes manifests |
| Ingress | NGINX Ingress Controller |
| Monitoring | Prometheus, Grafana |
| DNS | Hostinger, Ingress LoadBalancer |

---

## ⚡ CD Workflow Overview

1. **Kubernetes & ArgoCD Setup**
   - Installed ArgoCD using Helm on EKS cluster.
   - Configured declarative GitOps deployments.

2. **Application Deployment**
   - Created Kubernetes manifests (Deployment, Service, HPA, Ingress).
   - Defined ArgoCD Application declaratively.
   - Manual sync performed initially for resources.

3. **GitOps Integration**
   - CI pipeline updates feature branches → CD manifests updated automatically.
   - ArgoCD detects changes, syncs, and deploys updated images.

4. **DNS Configuration**
   - Ingress configured with host entry.
   - DNS record mapped via Hostinger.
   - Application accessible at custom domain.

5. **Monitoring Setup**
   - Prometheus & Grafana installed via Helm.
   - Scrapes metrics from ArgoCD and cluster resources.
   - Dashboards provide deployment performance and cluster health.

---

## 📝 Activity Logs

- All deployment steps, ArgoCD sync screenshots, and monitoring dashboards are stored in the `Activity-Logs-CD_Machine` folder in this CD repository.
- Provides visual confirmation of each stage of the pipeline.

---

## 🔧 Troubleshooting Highlights

- Kubernetes networking and HPA misconceptions addressed.
- Prometheus service initially inaccessible → added ServiceMonitor matching Helm release.
- ArgoCD resource sync errors resolved by manual initial sync.

---

## 🎯 Outcome

- Fully automated GitOps-based deployment workflow.
- Continuous updates from CI → CD seamlessly managed by ArgoCD.
- End-to-end monitoring and DNS-based application access ensured.

---

## 👤 Contributors

- **DevOps Implementation:** Danush Vithiyarth Jaiganesh  
- **Application Source:** [Boardgame](https://github.com/jaiswaladi246/Boardgame.git)  

---

> **Note:** This repository only handles **CD (deployment & monitoring)**. The **CI process** (build, test, push) is in the separate repository: [ArgoCD Project – CI Process](https://github.com/danushvithiyarth/ArgoCd-project-CI_Process.git)
