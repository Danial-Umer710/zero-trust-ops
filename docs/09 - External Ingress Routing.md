
# Phase 6: External Access (Ingress)

## 1. The Ingress Controller
A Service routes traffic *inside* the cluster. An Ingress acts as the front door, routing external internet traffic to the internal Services based on URL paths.
* **Execution:** Declared an Ingress to route external HTTP traffic to the internal `nginx-service`.

## 2. Firewalling the Front Door
Because of the Default Deny architecture, the Ingress Controller (Traefik) was initially blocked from reaching the NGINX pods.
* **The Fix:** Updated the `allow-nginx` NetworkPolicy to explicitly trust traffic originating from the `kube-system` namespace. This maintains Zero-Trust isolation while allowing the authorized front door to function.