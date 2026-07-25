
# Phase 7: eBPF Observability with Hubble

## 1. The Visibility Gap
A Zero-Trust network is blind by default. When standard `curl` commands time out, it is impossible to know if it is a network failure, a DNS issue, or a firewall block without deep inspection.

## 2. Enabling Hubble
Cilium Hubble was enabled to expose real-time eBPF packet flows.
* **Hubble Relay:** Hooks into the Linux kernel to read network maps.
* **Hubble UI:** Provides a visual, dynamic service map of all traffic.

## 3. Configuration Drift & Visual Verification
* **Dropped Traffic (Red):** The manual `access=granted` label applied to `test-client` via `kubectl` was wiped out upon cluster restart. This demonstrates Configuration Drift. Because the label was not stored in Git, the Default Deny policy correctly intercepted and destroyed the packets.
* **Forwarded Traffic (Green):** External traffic routed through `localhost:8000` successfully passed through Traefik to NGINX. The UI visually proved the GitOps network policy effectively read the `kube-system` namespace label and granted access.