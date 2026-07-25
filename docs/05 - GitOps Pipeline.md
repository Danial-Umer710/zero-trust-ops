
# Phase 3: Connecting the GitOps Pipeline

## 1. The Git Repository (Source of Truth)
Created a public GitHub repository named `zero-trust-ops`. In a GitOps architecture, this repository acts as the absolute state of the infrastructure. No manual `kubectl apply` commands are used in production; all infrastructure must be committed as code here.

## 2. Linking ArgoCD to GitHub
Configured ArgoCD to watch the repository using the Pull-based deployment model.
* **UI Path:** Settings > Repositories > + Connect Repo
* **Method:** HTTPS / Git
* **Target:** `https://github.com/<username>/zero-trust-ops.git`

## 3. Push vs. Pull Security Model
* **Legacy (Push/CIOps):** An external CI/CD server holds cluster admin credentials and pushes code in. Massive security risk if the CI server is breached.
* **Modern (Pull/GitOps):** ArgoCD sits inside the secure cluster network and pulls code from Git. The cluster has no open inbound management ports, and external servers hold zero cluster credentials.