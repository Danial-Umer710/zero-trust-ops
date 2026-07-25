
# Phase 3: The GitOps Engine

## 1. Install ArgoCD
ArgoCD implements the GitOps "pull" methodology. By running inside the cluster, it pulls deployments from Git, eliminating the need to expose cluster admin credentials to external CI/CD servers.

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f [https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml](https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```

## 2. Verify Deployment

Bash

```
kubectl get pods -n argocd
```

_Wait for all pods to reach the `Running` state._

## 3. Accessing the UI
The ArgoCD UI is not exposed externally by default. It requires a manual port-forward to access locally.

**Extract Initial Password:**
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo 

**Open the Tunnel:**
```
```
Bash


kubectl port-forward svc/argocd-server -n argocd 8080:443
password : p0uSHANegJ787MN5
```

_Access via `https://localhost:8080` (Username: `admin`). Bypass the self-signed SSL warning._ ```