
# Phase 11: Auto-Scaling (HPA)

## 1. Dynamic Resource Management
Static pod counts fail under sudden traffic spikes. Horizontal Pod Autoscalers (HPA) continuously read hardware metrics from the cluster's metrics-server to expand or contract the number of running containers based on real-time demand.

## 2. Configuration
Deployed an HPA via GitOps targeting the NGINX deployment:
* **Minimum Replicas:** 2 (High availability baseline)
* **Maximum Replicas:** 5 (Resource ceiling to prevent node exhaustion)
* **Target Metric:** 50% average CPU utilization

## 3. Destructive Verification
* Injected a CPU-intensive process (`cat /dev/zero > /dev/null`) directly into a running container to simulate a traffic surge.
* **Result:** HPA detected the spike (102% against a 50% target) and automatically provisioned new pods up to the maximum limit (5). This distributed the overall CPU load, successfully dropping the average cluster utilization back to a stable 42%.