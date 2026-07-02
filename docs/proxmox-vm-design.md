# Proxmox VM Design

## Purpose

This document defines the VM settings for the Talos Kubernetes nodes.

---

## VM Naming

| VM Name | Role | Proxmox Host |
|--------|------|--------------|
| talos-cp-1 | Control Plane | pve-node-3 |
| talos-worker-1 | Worker | pve-node-1 |
| talos-worker-2 | Worker | pve-node-2 |

---

## VM Resources

| VM | vCPU | Memory | Disk |
|---|---:|---:|---:|
| talos-cp-1 | 2 | 4 GB | 32 GB |
| talos-worker-1 | 2 | 4 GB | 64 GB |
| talos-worker-2 | 2 | 4 GB | 64 GB |

---

## Recommended VM Settings

| Setting | Value |
|--------|-------|
| BIOS | OVMF / UEFI |
| Machine | q35 |
| CPU Type | host |
| Disk Bus | VirtIO SCSI |
| Network | VirtIO |
| SCSI Controller | VirtIO SCSI single |
| Guest Agent | Disabled initially |
| Cloud-Init | Not used |
| Secure Boot | Disabled |

---

## Design Decisions

### Why UEFI?

UEFI is modern and commonly used for current Linux systems.

### Why q35?

q35 provides a modern virtual machine chipset and is a good default for new VMs.

### Why CPU type host?

Using `host` exposes the physical CPU features to the VM and usually provides better performance.

### Why VirtIO?

VirtIO drivers provide efficient virtualized disk and network performance.

### Why no Cloud-Init?

Talos is configured through machine configuration files and `talosctl`, not through traditional cloud-init.

---

## Future Improvements

- Increase worker RAM if application workloads require it
- Add more worker nodes
- Add three control plane nodes for high availability