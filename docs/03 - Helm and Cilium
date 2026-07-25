
# Phase 2: Core Infrastructure

## 1. Install Helm (Package Manager)
```bash
curl -fsSL -o get_helm.sh [https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3](https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3)
chmod 700 get_helm.sh
./get_helm.sh


## 2. Deploy Cilium (eBPF CNI)

Added the official repo and installed the network plugin into the `kube-system` namespace. This activates the cluster networking and transitions nodes to `Ready`.

Bash

```
helm repo add cilium [https://helm.cilium.io/](https://helm.cilium.io/)
helm repo update
helm install cilium cilium/cilium --namespace kube-system
```
