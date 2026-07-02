# Kubernetes Components

## Purpose

This document describes all major components used in the Talos Kubernetes cluster.

---

# Core Components

| Component | Purpose | Status |
|-----------|---------|--------|
| Talos Linux | Kubernetes operating system | Planned |
| Kubernetes | Container orchestration | Planned |
| Cilium | Container Network Interface (CNI) | Planned |
| CoreDNS | Internal cluster DNS | Planned |
| kube-proxy | Service networking | Managed by Kubernetes |

---

# Networking

| Component | Purpose |
|-----------|---------|
| Cilium | Pod networking |
| MetalLB | LoadBalancer implementation |
| Traefik | HTTP/HTTPS routing |
| cert-manager | TLS certificate management |

---

# Storage

| Component | Purpose |
|-----------|---------|
| NFS Server | Shared storage |
| NFS CSI Driver | Kubernetes storage integration |
| Persistent Volumes | Persistent application storage |

---

# GitOps

| Component | Purpose |
|-----------|---------|
| Flux CD | GitOps continuous reconciliation |

---

# Monitoring

| Component | Purpose | Status |
|-----------|---------|--------|
| Prometheus | Metrics collection | Future |
| Grafana | Dashboards | Future |
| Alertmanager | Alerting | Future |

---

# Applications

Applications will be migrated gradually.

Planned applications include:

- Homepage
- Jellyfin
- Crafty Controller
- Syncthing

---

# Design Decisions

## Why Talos?

Talos provides an immutable and API-driven operating system designed specifically for Kubernetes.

## Why Cilium?

Cilium offers a modern eBPF-based networking solution with excellent observability and security features.

## Why Flux CD?

Flux CD continuously synchronizes the desired cluster state from Git and integrates naturally into a Git-centric workflow.

## Why NFS?

The existing infrastructure already provides an NFS server, making it the simplest and most reliable storage backend for the initial cluster.

---

# Future Improvements

- Prometheus
- Grafana
- cert-manager
- External Secrets
- Renovate
- Kyverno (optional)

---

# Lessons Learned

A Kubernetes cluster consists of multiple independent components, each solving a specific problem.