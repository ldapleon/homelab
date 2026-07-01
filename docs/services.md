# Services Inventory

## Purpose

This document lists all services currently running in the homelab and their planned migration path.

---

# Current Services

| Service | Host | Technology | Purpose | Planned Migration |
|----------|------|------------|---------|-------------------|
| CasaOS | pve-node-1 | LXC | Docker Host | Replace |
| Jellyfin | CasaOS | Docker | Media Server | Kubernetes |
| Crafty Controller | CasaOS | Docker | Minecraft Management | Kubernetes |
| Portainer | CasaOS | Docker | Docker Management | Remove after migration |
| Pi-hole | pve-node-2 | LXC | DNS Server | TBD |
| Nginx Proxy Manager | pve-node-2 | LXC | Reverse Proxy | Replace with Ingress |
| Syncthing | pve-node-2 | LXC | File Synchronization | Kubernetes |
| Homepage | LXC | Docker | Dashboard | Kubernetes |

---

# Migration Strategy

## Replace

- CasaOS
- Nginx Proxy Manager

## Migrate

- Jellyfin
- Crafty Controller
- Homepage
- Syncthing

## Evaluate

- Pi-hole

---

# Dependencies

## Jellyfin

Needs:

- NFS Storage
- Media Library
- GPU / Intel QuickSync (optional)

---

## Crafty Controller

Needs:

- Persistent Storage
- Minecraft Server Files

---

# Lessons Learned

- Most application workloads are containerized already.
- Infrastructure services are separated from application services.
- Kubernetes migration can be performed incrementally.