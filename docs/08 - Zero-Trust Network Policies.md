
# Phase 5: Zero-Trust Network Policies

## 1. Default Deny Architecture
By default, Kubernetes uses a flat network. To secure the cluster, a baseline `NetworkPolicy` was applied to drop all incoming (`Ingress`) traffic across the namespace:
* **Effect:** Isolates all pods completely. No pod can communicate with another pod unless explicitly permitted.

## 2. Identity-Based Microsegmentation
Rather than relying on IP addresses (which constantly change in Kubernetes), rules are declared using pod labels.

* **Policy:** `allow-nginx`
* **Target:** Pods labeled `app: nginx`
* **Rule:** Allow inbound TCP traffic on port 80 ONLY from pods labeled `access: granted`.

## 3. Dynamic Enforcement
* Without label `access: granted`: Request drops / times out (Exit Code 28).
* With label `access: granted`: Request succeeds instantly without pod restarts.