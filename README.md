![Helm](https://img.shields.io/badge/helm-v3-blue)

# Fastboot Platform Helm Chart

Helm chart for deploying the Fastboot Platform (IDP) on Kubernetes.

## 🚀 Overview

This chart installs:

* Fastboot Platform backend
* Kubernetes resources (Deployment, Service, etc.)
* Optional secrets and configuration

---

## 📦 Prerequisites

* Kubernetes 1.33+
* Helm 3.x
* Access to container registry (`ghcr.io`)

---

## 📥 Installation

### 1. Add registry (if using OCI)

```bash
helm registry login ghcr.io -u <your-username>
```

### 2. Install the chart

```bash
helm install fastboot oci://ghcr.io/fastboot-io/fastboot-idp-helm-chart --set artifactory.enabled=false -n fastboot
```

---

## ⚙️ Configuration

You can override values using** **`values.yaml` or** **`--set`.

### Example:

```bash
helm install fastboot oci://ghcr.io/fastboot-io/fastboot-idp-helm-chart \
  --set artifactory.enabled=false \
  --set image.tag=1.0.0 \
  --set service.port=8080 -n fastboot
```

---

## 🔐 Secrets

Do NOT store real credentials in** **`values.yaml`.

### Example (Use existing Kubernetes Secret)

```yaml
existingSecret: artifactory-secret
```

---

## 📁 Values


| Key                               | Description        | Default                      |
| --------------------------------- | ------------------ | ---------------------------- |
| operator.image.repository         | Container image    | ghcr.io/fastboot-io/platform |
| operator.image.tag                | Image tag          | 1.0.0                        |
| operator.deployment.replicas      | Replicas           | 1                            |
| operator.service.type             | Service type       | ClusterIP                    |
| operator.service.port             | Service port       | 8080                         |
| operator.ingress.ingressClassName | Ingress class name | nginx                        |
| artifactory.secretName            | Artifactory secret | artifactory-secret           |

---

## 🔄 Upgrading

```bash
helm upgrade fastboot oci://ghcr.io/fastboot-io/fastboot-idp-helm-chart -n fastboot
```

---

## 🗑️ Uninstall

```bash
helm uninstall fastboot -n fastboot
```

---

## 🧱 Chart Structure

```
platform-helm/
├── Chart.yaml
├── values.yaml
├── crds/
├── environments/
│   ├── local-values.yaml
│   ├── onprem-values.yaml
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── secret.yaml
│   └── ...
```

---

## 🛡️ Notes

* All templates are public and contain no sensitive data
* Provide secrets at install time
* Designed for extensibility and production use

---

## 🤝 Contributing

Feel free to open issues or PRs to improve the chart.
