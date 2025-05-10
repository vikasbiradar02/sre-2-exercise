# 📊 SRE-2 Take-Home: Scalable & Secure Observability Stack on Kubernetes

This repository is the submission for the SRE-2 take-home exercise. It implements a scalable, secure, and production-ready observability stack for Kubernetes, deployed using Helm and structured according to Infrastructure-as-Code (IaC) principles.

---

## 📌 Summary

This observability platform includes centralized monitoring and logging for workloads running across a Kubernetes cluster. It supports:

- **Metrics** with Prometheus and Alertmanager
- **Logs** with Fluent Bit and Loki
- **Visualization** via Grafana
- **Security** through RBAC and NetworkPolicies
- **Optional GitOps** via ArgoCD

---

## 📐 Architecture Overview

**Tools Used:**
- **Prometheus** (metrics & alerts)
- **Loki** (log aggregation)
- **Fluent Bit** (log shipping)
- **Grafana** (dashboards)
- **Alertmanager** (alert routing)
- **ArgoCD** (optional GitOps deployment)

**Design Principles:**
- Pull-based metrics scraping by Prometheus
- Log ingestion with Fluent Bit → Loki
- Namespace-scoped RBAC for team separation
- NetworkPolicies to restrict cross-namespace traffic
- Helm values files for modular deployments

**Assumptions:**
- Cluster access with `kubectl` and `helm`
- Namespace `observability` will host all components

---

## 📁 Directory Structure

```bash
observability-stack/
├── charts/
│   ├── prometheus/       # Prometheus & AlertManager Helm values
│   ├── grafana/          # Grafana dashboards, datasources
│   ├── loki/             # Loki configuration
│   └── fluent-bit/       # Fluent Bit pipeline values
├── rbac/
│   └── observability-rbac.yaml
├── network-policies/
│   └── restrict-ns-traffic.yaml
├── alerts/
│   └── high-cpu.yaml     # Example alert rule
├── argocd(gitops)/
│   └── prometheus-app.yaml
├── README.md             # This file
└── observability_deployment_steps.docx  # Full step-by-step guide
⚙️ Deployment Instructions

📎 Prerequisites
A Kubernetes cluster
kubectl configured (kubectl get nodes)
Helm v3 installed (helm version)
Optional: ArgoCD installed
🧪 Setup
git clone https://github.com/your-org/observability-stack.git
cd observability-stack
Step 1: Create Namespace
kubectl create namespace observability
kubectl label namespace observability access=observability
Step 2: Add Helm Repos
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add fluent https://fluent.github.io/helm-charts
helm repo update
Step 3: Install Components
# Prometheus + AlertManager
helm install prometheus prometheus-community/kube-prometheus-stack \
  -f charts/prometheus/values.yaml -n observability

# Loki
helm install loki grafana/loki \
  -f charts/loki/values.yaml -n observability

# Fluent Bit
helm install fluent-bit fluent/fluent-bit \
  -f charts/fluent-bit/values.yaml -n observability

# Grafana
helm install grafana grafana/grafana \
  -f charts/grafana/values.yaml -n observability
Step 4: Access Grafana Locally
kubectl port-forward svc/grafana 3000:80 -n observability
# Visit http://localhost:3000 (default user: admin/admin or per values.yaml)
🔐 Security Configurations

RBAC
kubectl apply -f rbac/observability-rbac.yaml
Network Policy
kubectl apply -f network-policies/restrict-ns-traffic.yaml
🚨 Alerts (Optional)

kubectl create configmap cpu-alerts \
  --from-file=alerts/high-cpu.yaml -n observability

kubectl label configmap cpu-alerts role=alert-rules -n observability
🔄 GitOps with ArgoCD (Optional)

kubectl apply -f argocd/prometheus-app.yaml
Once applied, ArgoCD will monitor the Git repository and keep Prometheus deployments in sync.

✅ Validation

kubectl get pods -n observability
Ensure all observability components (prometheus, grafana, loki, fluent-bit) are running.

