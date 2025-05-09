# 🛠 Take-Home Exercise: Scalable & Secure Observability Stack on Kubernetes

## Context
Your organization is building a centralized observability platform for monitoring and logging across multiple Kubernetes workloads. The platform should be scalable, secure, and aligned with infrastructure-as-code (IaC) best practices.

You are tasked with designing and provisioning this observability stack using tools of your choice (e.g., Prometheus, Grafana, Loki, Fluent Bit, Elasticsearch, etc.). Assume the Kubernetes cluster already exists and hosts multiple services in different namespaces.

---

## ✅ Objectives

### 1. Design Document (1–2 pages)
- Describe the architecture of your observability stack.
- Explain:
  - How it will scale with increasing workloads and tenants.
  - How you will secure access (e.g., RBAC, TLS, network policies).
  - Any trade-offs or assumptions made (e.g., log retention, data volume, pull vs push metrics).
- Optionally, mention how the solution could evolve in a production-grade environment.

### 2. IaC Code (Terraform or Helm preferred)
- Provide code to:
  - Deploy the observability stack (minimum: metrics and logging).
  - Apply RBAC policies to restrict access to observability data per namespace or team.
  - Configure basic network restrictions (e.g., using Kubernetes NetworkPolicy or security groups).
- You can use Helm charts or Terraform modules, but avoid raw kubectl commands unless absolutely necessary.

### 3. Optional (Bonus)
- Define a simple alert rule for one workload (e.g., CPU threshold breach).
- Include a brief note on how this setup could be automated or managed via GitOps (e.g., using ArgoCD or Flux).

---

## 📦 Deliverables
- A Git repository (or ZIP file) containing:
  - A `README.md` that explains your approach, design decisions, and how to apply the IaC code.
  - IaC code directory with Terraform/Helm files.

---

## ⏱ Time Expectation
- 2–4 hours.
- Focus on clarity and reasoning. We're more interested in **how** you approach the problem than a production-ready deployment.
