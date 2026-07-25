
# Phase 13: Advanced Observability

## 1. The Telemetry Stack
Operating a cluster without observability is flying blind. We deployed the kube-prometheus-stack using Helm via ArgoCD. This provides enterprise-grade metrics scraping and visualization without manual configuration.

## 2. Components
* **Prometheus:** The time-series database that scrapes hardware and application metrics from the cluster's nodes and pods.
* **Grafana:** The visualization engine that queries Prometheus to build real-time dashboards for CPU, memory, network, and application health.

## 3. Verification
* Successfully accessed Grafana via secure port-forwarding.
* Verified that the declarative hardware limits (50m request / 100m limit) applied in previous GitOps deployments are actively enforced and visible on the compute resource dashboards.