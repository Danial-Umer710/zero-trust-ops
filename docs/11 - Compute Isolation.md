
# Phase 8: Compute Isolation (Resource Limits)

## 1. The Hardware Blast Radius
Without strict hardware constraints, a single compromised or malfunctioning container can consume 100% of the underlying node's CPU and RAM, crashing the entire Kubernetes cluster.

## 2. Requests vs. Limits
Applied Linux cgroup constraints via the GitOps Deployment manifest:
* **Requests (`64Mi`):** The guaranteed minimum memory required to schedule the pod.
* **Limits (`128Mi`):** The absolute maximum memory allowed. 

## 3. Destructive Verification
* Executed an infinite memory-consumption loop via `awk` directly inside the pod.
* **Result:** The kernel successfully intercepted the breach, terminated the process with `Exit Code 137 (SIGKILL)`, and flagged the pod as `OOMKilled`. Kubernetes immediately auto-healed the deployment by spinning up a fresh replica.