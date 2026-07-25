
# Phase 1: Environment Setup & Core Tools

## 1. Starting Docker in WSL
WSL does not auto-start services. After every Windows reboot, Docker must be started manually:
```bash
sudo service docker start
```
*If Docker gives a permission denied error, force read/write access:*
```bash
sudo chmod 666 /var/run/docker.sock
```

## 2. Installing Kubernetes Remote Control (kubectl)
```bash
curl -LO "[https://dl.k8s.io/release/$(curl](https://dl.k8s.io/release/$(curl) -L -s [https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl](https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl)"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

## 3. Installing the Local Cluster Engine (k3d)
```bash
curl -s [https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh](https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh) | bash
