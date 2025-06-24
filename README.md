# 🚀 Multi-App API Helm Chart

This repository contains a Helm chart to deploy a **multi-language API stack** powered by:

- **Go**
- **.NET**
- **Node.js (Express)**
- **Ruby on Rails**

All services are reverse-proxied through **NGINX** and exposed under distinct API paths (`/go`, `/dotnet`, `/nodejs`, `/rails`).  
This Helm chart is designed to run in **Kubernetes** environments (e.g. via **Rancher**) with **SSL/TLS handled by the ingress controller**.

---

## 📁 Project Structure

```
greeting-apis/
├── charts/
├── templates/
│   ├── go-api-deployment.yaml
│   ├── dotnet-api-deployment.yaml
│   ├── nodejs-api-deployment.yaml
│   ├── rails-api-deployment.yaml
│   ├── nginx-deployment.yaml
│   └── ingress.yaml
├── values.yaml
├── Chart.yaml
```

---

## ⚙️ Configuration

Customize the deployment values in [`values.yaml`](./values.yaml):

```yaml
dotnet:
  image: balenabdalla/dotnet-greeting-api
  tag: latest

go:
  image: balenabdalla/go-greeting-api
  tag: latest

nodejs:
  image: balenabdalla/nodejs-greeting-api
  tag: latest

rails:
  image: balenabdalla/rails-greeting-api
  tag: latest
  env:
    SECRET_KEY_BASE: your-secret-here
```

---

## 🚢 Deployment Instructions

### 🛠 Prerequisites

- A running Kubernetes cluster (via Rancher or other)
- Helm installed and configured locally
- Docker images pushed to a container registry (e.g., Docker Hub)
- A Kubernetes namespace (you can view/create this via Rancher or CLI)

### 📦 Install the chart

```bash
helm install greeting-apis ./greeting-apis --namespace <your-namespace>
```

> 💡 Replace `<your-namespace>` with the name of your target Kubernetes namespace.

---

## 🌐 API Access

Once deployed, access each API at:

```
https://your-domain.com/go
https://your-domain.com/dotnet
https://your-domain.com/nodejs
https://your-domain.com/rails
```

> The NGINX ingress will route requests based on path prefixes to each API.

---

## 🧪 Monitoring & Logs

Check the status of the pods:

```bash
kubectl get pods -n <your-namespace>
```

View logs for a specific API:

```bash
kubectl logs -f <pod-name> -n <your-namespace>
```

## 💬 Support

Feel free to open an [issue](https://github.com/balen-dev/Greeting_APIs/issues) or submit a [pull request](https://github.com/balenabdalla/Greeting_APIs/pulls) if you have improvements or questions!
