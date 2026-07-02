# Cluster Design

## Purpose

This document describes the physical and logical design of the Talos Kubernetes cluster.

## Cluster Topology

| VM                | Host         | Role          | vCPU |  RAM |  Disk |
| ----------------- | ------------ | ------------- | ---: | ---: | ----: |
| `talos-cp-01`     | `pve-node-3` | Control Plane |    2 | 4 GB | 32 GB |
| `talos-worker-01` | `pve-node-1` | Worker        |    2 | 4 GB | 64 GB |
| `talos-worker-02` | `pve-node-2` | Worker        |    2 | 4 GB | 64 GB |




## Design Decisions

### Why one Control Plane?

For my current learning environment, a single control plane node is sufficient. It keeps the cluster simple, reduces resource usage and can easily be expanded to a highly available three-node control plane later.

### Why this VM placement?

The third Proxmox node currently hosts no virtual machines or containers. Apart from Proxmox itself, the system mainly provides the NFS share. This makes it a suitable location for the Talos control plane VM.

### Resource Allocation

The initial resource allocation is intentionally conservative. Kubernetes allows resources to be adjusted later if workloads require additional CPU or memory.

## Future Improvements

- Three control plane nodes
- High Availability
- Additional worker nodes