
# Phase 9: Application Health Checks (Probes)

## 1. The Container Illusion
A container can report a `Running` state even if the application inside it is completely frozen or returning 500 Server Errors. Kubernetes needs to be configured to actively interrogate the application layer.

## 2. Probe Definitions
Configured HTTP GET probes to ensure the application is responding with 200 OK HTTP codes.
* **Liveness Probe:** The restart switch. Kubernetes will ping your website every 10 seconds. If it doesn't get a 200 OK response, it assumes the app is frozen and assassinate the pod.
* **Readiness Probe:** The traffic switch. When a new pod boots up, Kubernetes won't send any traffic to it until this probe passes, ensuring users never hit a half-booted application.

## 3. Destructive Verification
* Intentionally deleted the `index.html` file inside the running NGINX container.
* **Result:** The Liveness probe began receiving HTTP 403 errors instead of 200 OK. After failing the consecutive threshold, Kubernetes automatically terminated the broken pod and spun up a fresh replica to restore service.