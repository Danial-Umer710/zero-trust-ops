
# Phase 4: Application Deployment & Services

## 1. Kubernetes Deployments (The Pod Manager)
A Deployment does not run code; it manages pods. It ensures a specific number of pod replicas are running at all times. It tracks these pods using identity labels.

* **Key Concept:** We do not deploy pods manually. We declare a Deployment, and the Deployment stamps out the pods using a template.
* **GitOps Execution:** Committed `nginx.yaml` to GitHub. ArgoCD automatically detected the change and spun up 2 NGINX pods.

## 2. Kubernetes Services (The Internal Load Balancer)
Pods are ephemeral and their IP addresses change constantly. A Service provides a permanent, static IP address and DNS name. 

* **Key Concept:** The Service acts as a static entry point. It uses "Selectors" to find pods with matching labels (e.g., `app: nginx`) and distributes traffic across them.
* **GitOps Execution:** Committed `nginx-service.yaml` to GitHub. ArgoCD built the Service, permanently linking the internal cluster network to the disposable pods.