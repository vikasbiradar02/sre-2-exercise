# SRE-2 Take Home: Observability on Kubernetes

Clone this repo , make your changes, commit them with proper commit logs , and share the zipped file as submission.
Don't fork and publish your submission in public .

## 📌 Summary

This repository contains my submission for the take-home exercise to design and deploy a scalable, secure observability stack on Kubernetes using infrastructure-as-code.

---

## 📐 Architecture Design

- Tools used: (e.g., Prometheus, Grafana, Loki, Fluent Bit)
- Design overview:
  - Metrics pipeline:
  - Logging pipeline:
  - Access control & RBAC:
  - Network policies:
- Scalability strategy:
- Security considerations:
- Trade-offs and assumptions:

(Detailed explanation can go in `design/architecture.md` if preferred.)

---

## ⚙️ How to Apply This Code

### Prerequisites
- Kubernetes cluster
- Helm 3 / Terraform CLI
- kubeconfig access

### Deployment Steps

1. Clone this repo:
   ```bash
   git clone <your-fork-url>
   cd sre-observability-takehome
   ```

2. Deploy the observability stack:
   ```bash
   # Using Helm
   cd iac/helm
   helm install observability-stack . -f values.yaml

   # Or using Terraform
   cd iac/terraform
   terraform init
   terraform apply
   ```

3. (Optional) Apply network policies:
   ```bash
   kubectl apply -f ./network-policies.yaml
   ```

---

## 🚨 Alerts (Optional)

- Alert Rule: `high_cpu_usage.yaml`
- Alertmanager configuration: `extras/alertmanager.yaml`

---

## 🔄 GitOps (Optional)

Brief description of how this setup could be managed using a GitOps tool like ArgoCD or Flux.

---

## 📁 Repository Layout

```
├── problem.md
├── design/
├── iac/
├── extras/
└── README.md
```

---

## ⏱ Estimated Time

~2–4 hours total.
