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

