# Networking Design

## Purpose

This document describes the networking design for the Talos Kubernetes cluster.

---

## Network Layers

The cluster uses multiple network layers:

| Layer | Purpose |
|------|---------|
| Home Network | Physical LAN and access to the cluster |
| Talos Node Network | IP addresses of the Kubernetes nodes |
| Pod Network | Internal communication between pods |
| Service Network | Stable virtual IPs for Kubernetes services |
| LoadBalancer Network | External IPs exposed to the home network |
| Ingress | HTTP/HTTPS routing to applications |

---

## Home Network

| Setting | Value |
|--------|-------|
| Network | 192.168.188.0/24 |
| Gateway | 192.168.188.1 |
| Router | Fritz!Box |
| DNS | Pi-hole |
| DHCP | Fritz!Box |

---

## Planned Talos Node IPs

| Node | Role | IP Address | Status |
|-----|------|------------|--------|
| talos-cp-01 | Control Plane | TBD | Planned |
| talos-worker-01 | Worker | TBD | Planned |
| talos-worker-02 | Worker | TBD | Planned |

The Talos nodes require static IP addresses or DHCP reservations.

---

## Kubernetes Pod Network

| Setting | Value |
|--------|-------|
| Pod CIDR | 10.244.0.0/16 |
| Managed By | Cilium |

Pods receive internal cluster IP addresses from this range.

---

## Kubernetes Service Network

| Setting | Value |
|--------|-------|
| Service CIDR | 10.96.0.0/12 |

Services provide stable virtual IP addresses inside the cluster.

---

## LoadBalancer Network

MetalLB will provide external IP addresses from the home network.

| Setting | Value |
|--------|-------|
| MetalLB Pool | TBD |
| Purpose | Expose services to the LAN |

Example future pool:

```text
192.168.188.xxx - 192.168.188.xxx