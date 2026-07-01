# Hardware Inventory

## Overview

| Node | Model | CPU | RAM | Storage | Purpose |
|------|-------|-----|-----|---------|---------|
| pve01 | HP ProDesk 400 G5 Mini | Intel Core i5 | 16 GB | 256 GB SSD | CasaOS / Docker |
| pve02 | Lenovo Mini PC | AMD CPU | 16 GB | 256 GB SSD | Infrastructure Services |
| pve03 | Intel NUC | Intel Core i5 | 8 GB | 256 GB SSD (System) + 2 TB SSD | Storage / Future Kubernetes |

---

## Node Details

### pve01

**Hostname**
- pve01

**Hardware**
- HP ProDesk 400 G5 Mini
- Intel Core i5
- 16 GB RAM
- 256 GB SSD

**Current Services**
- CasaOS
- Jellyfin
- Crafty Controller
- Portainer
- Other Docker containers

---

### pve02

**Hostname**
- pve02

**Hardware**
- Lenovo Mini PC
- AMD CPU
- 16 GB RAM
- 256 GB SSD

**Current Services**
- Pi-hole
- Nginx Proxy Manager
- Syncthing

---

### pve03

**Hostname**
- pve03

**Hardware**
- Intel NUC
- Intel Core i5
- 8 GB RAM
- 256 GB SSD
- 2 TB SSD

**Current Services**
- NFS Share

**Planned Purpose**
- Kubernetes Worker
- NFS Storage