# Backup Strategy

## Purpose

This document describes the current and future backup strategy for the homelab.

The primary goals are:

- Protect critical data
- Minimize downtime
- Enable disaster recovery
- Ensure recoverability after hardware failures

---

# Backup Philosophy

Backups should follow the **3-2-1 principle** whenever possible:

- 3 copies of important data
- 2 different storage media
- 1 copy stored off-site

The current homelab does not yet fully implement this strategy but will gradually evolve towards it.

---

# Current Backup Strategy

## Proxmox

| Item | Method | Frequency | Status |
|------|--------|-----------|--------|
| Virtual Machines | Manual Backup | On Demand | Current |
| LXC Containers | Manual Backup | On Demand | Current |

---

## Media Storage

| Storage | Backup | Status |
|----------|--------|--------|
| Jellyfin Media | No Backup | Planned |

Large media files can be restored from the original source if necessary.

---

## Configuration Files

| Item | Backup |
|------|--------|
| Pi-hole | Manual Export |
| Nginx Proxy Manager | Manual |
| CasaOS | Manual |
| Git Repository | GitHub |

---

# Future Backup Strategy

## Proxmox

- Scheduled VM backups
- Scheduled LXC backups
- Backup retention policy

---

## Kubernetes

Future backups will include:

- Persistent Volumes
- Kubernetes manifests
- Talos configuration
- GitOps repository

Possible tools:

- Velero
- Proxmox Backup Server (future)
- Restic

---

# Disaster Recovery Plan

## Scenario 1

### Proxmox Host Failure

Recovery steps:

1. Replace hardware
2. Install Proxmox VE
3. Restore VMs/LXCs
4. Verify services

---

## Scenario 2

### Kubernetes Cluster Failure

Recovery steps:

1. Deploy Talos nodes
2. Bootstrap Kubernetes
3. Restore GitOps configuration
4. Restore Persistent Volumes
5. Verify applications

---

## Scenario 3

### Accidental Data Deletion

Recovery steps:

1. Restore affected files
2. Verify integrity
3. Restart application if required

---

# Design Decisions

## Why Git is Important

Infrastructure configuration will be stored in Git.

This allows the Kubernetes cluster to be recreated quickly after a disaster.

---

## Why Separate Application Data

Application data should remain independent from the application itself.

Containers can always be recreated.

User data cannot.

---

# Future Improvements

- Deploy Proxmox Backup Server
- Automate scheduled backups
- Implement off-site backups
- Regular restore testing
- Backup monitoring

---

# Lessons Learned

- Backups are part of the infrastructure design.
- Recovery procedures are as important as the backups themselves.
- Infrastructure should always be reproducible.