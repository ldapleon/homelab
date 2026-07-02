# Kubernetes Design

## Purpose

This document describes the design decisions for the Kubernetes cluster.

---

# Design Goals

- Learn Kubernetes fundamentals
- Build a production-inspired homelab
- Keep the architecture simple
- Use reproducible infrastructure
- Migrate existing Docker workloads step by step

---

# Why Kubernetes?

Kubernetes has fascinated me for a long time and I love the flexibility and the skills you can learn from a project like this.
I also like the declarative infrastructure and loadbalancing properties.

---

# Why Talos Linux?

I chose Talos because it has a really radical yet interesting approach and I want to dig deeper into that.
Also it is easy to do upgrades and the documentation / the community is amazing.

---

# Why Virtual Machines?

Talos expects a full machine / VM, so a LXC would not be sufficient.

---

# Design Principles

- Keep it simple
- Infrastructure as Code
- Documentation first
- Reproducibility



                Proxmox Cluster

       pve-node-1
           │
           └── talos-cp-01

       pve-node-2
           │
           └── talos-worker-01

       pve-node-3
           │
           └── talos-worker-02

                    │

            Kubernetes Cluster
                    │
      ┌─────────────┼─────────────┐
      │             │             │
 Applications   Networking    Monitoring
                    │
               NFS Storage