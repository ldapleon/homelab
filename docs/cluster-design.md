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

For my purposes right now, it is sufficient and it is always good to start small and scale up later.

### Why this VM placement?

My third PVE node has no VMs or Containers at the moment and only the SSD is used for NFS. 
There it would be a good place to put the controlplane node.

### Resource Allocation

Like I said, it is better to start small and scale up later if needed. For my learning purposes the ressoruces should be enough.

## Future Improvements

- Three control plane nodes
- High Availability
- Additional worker nodes