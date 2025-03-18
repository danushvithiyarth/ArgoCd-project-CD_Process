# ArgoCD Project - CD Process

## Introduction

This repository focuses on the Continuous Deployment (CD) process using GitOps methodology with ArgoCD. The goal is to deploy containerized applications to a Kubernetes cluster using a fully automated pipeline.

This repository contains Kubernetes manifests, ArgoCD declarative configurations, and Activity logs of all setup including monitoring setups. It works in conjunction with the CI Process Repository, where the application is built, tested, and pushed to DockerHub. Additionally, a DNS configuration has been implemented to allow application access through a custom domain.

## Technologies Used

Amazon EKS (Elastic Kubernetes Service) - Managed Kubernetes cluster

ArgoCD - GitOps-based continuous deployment

Kubernetes - Container orchestration

Helm - Package manager for Kubernetes (used for installing ArgoCD, Prometheus, and Grafana)

Nginx Ingress Controller - To manage ingress traffic

Hostinger - DNS provider (used to purchase and configure "danushvithiyarth.in")

Prometheus & Grafana - Monitoring and visualization of Kubernetes metrics

## Workflow

### 1. Setting Up Kubernetes & ArgoCD

- Deployed an EKS Cluster in AWS.

- Installed ArgoCD using Helm.

- Configured ArgoCD for declarative application deployment.

- Deployed Nginx Ingress Controller to manage external traffic.

### 2. Deploying the Application with ArgoCD

- Created Kubernetes manifests under the manifest/ directory.

- Included Deployment, Service, HPA, and Ingress configurations.

- Defined an ArgoCD application declaratively under declarative-setup/.

- Used kubectl to create the ArgoCD application.

- Initially, resources were out of sync, so they were manually synced in ArgoCD.

### 3. Implementing GitOps Methodology

- Introduced a feature branch (feature-1) in the CI Process Repository to modify application code.

- Implemented additional Jenkins stages to:

  * Build and push a new image for the feature branch.

  * Test the updated application before merging.

- Upon approval, merged the feature branch into main.

- A final Jenkins stage automatically updated the CD Process Repository (manifest/deployment.yaml) with the new image tag.

- ArgoCD detected the change, marked the application as out of sync, and after manual sync, it deployed the updated version.

### 4.DNS Configuration for Application Access

- Updated the Kubernetes Ingress configuration to include a host entry.

- Added the DNS name to the Ingress file and mapped the Ingress Load Balancer link in the DNS record using Hostinger.

- Outcome: The application became accessible via the configured DNS name over the internet.

### 5.Monitoring with Prometheus & Grafana

- Installed Prometheus & Grafana via Helm.

- Configured Prometheus to scrape metrics from ArgoCD.

- Created a Grafana dashboard to visualize deployment performance and cluster health.

## Troubleshooting

### 1.Kubernetes Networking Misconceptions

- Private/public subnet segmentation is not always needed as Service types and Network Policies manage access control.

- Application Gateway Service (AGS) is not mandatory when using Kubernetes Ingress controllers like NGINX, ALB, or Traefik.

- Horizontal Pod Autoscaler (HPA) is for scaling pods and does not manage ingress traffic.

### 2.Prometheus Service Accessibility Issue:

- Installed Prometheus and Grafana using the Kube-stack Prometheus Helm chart.

- Grafana was accessible over the internet, but Prometheus was not.

- Possible Cause: Service misconfiguration for Prometheus.

- Workaround: Since Prometheus was still running, added a ServiceMonitor resource matching the Helm release name.

- Outcome: Prometheus pulled ArgoCD metrics and sent them to Grafana, ensuring metrics were visible on the dashboard.

## Contributors & Credits

DevOps Implementation: Danush Vithiyarth Jaiganesh - DevOps Engineer

Application Source Code: Boardgame Repository - "https://github.com/jaiswaladi246/Boardgame.git"

GitOps Automation & Infrastructure as Code: Danush Vithiyarth Jaiganesh - DevOps Engineer

## Note:
This repository focuses on GitOps-driven Continuous Deployment (CD) process using Kubernetes and ArgoCD. The CI process (building and testing the application) is handled in the CI Process Repository - "https://github.com/danushvithiyarth/ArgoCd-project-CI_Process.git".
