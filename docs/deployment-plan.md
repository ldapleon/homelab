# Deployment Plan

## Purpose

This document defines the deployment sequence for the Talos Kubernetes cluster.

---

# Phase 1

## Prepare Proxmox

- Download latest Talos image
- Upload image to Proxmox
- Verify storage
- Verify networking

---

# Phase 2

## Create Virtual Machines

- talos-cp-1
- talos-worker-1
- talos-worker-2

Verify:

- CPU
- Memory
- Network
- Disk

---

# Phase 3

## Generate Talos Configuration

- Generate secrets
- Generate machine configuration
- Configure endpoints
- Configure node IPs

---

# Phase 4

## Bootstrap Cluster

- Apply machine configuration
- Bootstrap etcd
- Retrieve kubeconfig

Verification:

- kubectl get nodes

---

# Phase 5

## Core Infrastructure

Install:

- Cilium
- MetalLB
- Traefik
- cert-manager
- Flux CD
- NFS CSI Driver

Verification:

- All pods running
- Nodes Ready

---

# Phase 6

## First Test Application

Deploy:

- whoami

Verify:

- Pod
- Service
- Ingress
- DNS

---

# Phase 7

## Monitoring

Install:

- Prometheus
- Grafana

---

# Phase 8

## Application Migration

Deploy gradually:

- Homepage
- Syncthing
- Crafty Controller
- Jellyfin

---

# Success Criteria

The deployment is considered successful if:

- All nodes are Ready
- Cilium is healthy
- Traefik serves applications
- Flux CD syncs successfully
- Persistent storage works