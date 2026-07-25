[02 - Cluster Creation.md](https://github.com/user-attachments/files/30373736/02.-.Cluster.Creation.md)

# Phase 1: Cluster Creation

## 1. Build the K3d Sandbox
Created a lightweight Kubernetes cluster named 'zero-trust'. 
*CRITICAL: The default Flannel network and network policies were disabled (`none`) to prevent conflicts with our eBPF CNI (Cilium).*

```bash
k3d cluster create zero-trust --k3s-arg "--flannel-backend=none@server:*" --k3s-arg "--disable-network-policy@server:*"
