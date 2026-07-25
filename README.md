# Zero-Trust GitOps Kubernetes Architecture

## Overview
This repository contains the declarative infrastructure and application configuration for a production-grade, self-healing Kubernetes environment. It demonstrates modern DevSecOps principles, transitioning from manual cluster management to a fully automated, Git-driven architecture. 

The physical cluster is completely ephemeral. All state, network policies, compute limits, and telemetry configurations are maintained in this repository and continuously synchronized via ArgoCD.

## Tech Stack
* **Cluster Engine:** k3d / Docker
* **Continuous Deployment (GitOps):** ArgoCD
* **Network & Security (eBPF):** Cilium
* **Ingress Controller:** Traefik
* **Observability:** Prometheus & Grafana (Helm)
* **Application:** NGINX

## Core Features Implemented

### 1. GitOps & Disaster Recovery
* Infrastructure as Code (IaC) is enforced using ArgoCD.
* The cluster runs on a continuous reconciliation loop, instantly detecting state drift.
* Successfully tested for Total Disaster Recovery: a complete namespace wipe (`kubectl delete all`) is automatically rebuilt from the GitHub repository in under 60 seconds without human intervention.

### 2. Zero-Trust Networking (eBPF)
* Replaced the standard `kube-proxy` with Cilium for high-performance, eBPF-based networking.
* Enforced default-deny network policies across all namespaces. 
* Traffic is explicitly whitelisted; unauthorized internal lateral movement (simulated via internal hacker pods) is dropped at the Linux kernel level.

### 3. Compute Isolation & Auto-Scaling
* Strict CPU and Memory limits/requests are enforced on all containers to prevent node starvation and noisy-neighbor issues.
* Horizontal Pod Autoscaler (HPA) configured to dynamically scale worker pods based on real-time CPU metric thresholds.
* Tested against simulated DoS (infinite-loop CPU spikes), proving automated scaling and load stabilization.

### 4. Advanced Observability
* Deployed the enterprise `kube-prometheus-stack` via ArgoCD using remote Helm charts.
* Real-time metrics scraping of kernel, node, and pod hardware utilization.
* Monitored via Grafana dashboards to verify quota enforcement, network flow, and scaling events.

## Documentation & Setup
Detailed architectural breakdowns, step-by-step setup guides, and destructive verification tests are documented in the `/docs` directory.
