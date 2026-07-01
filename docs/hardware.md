# Hardware Inventory

## Overview

| Node | Model | CPU | RAM | Storage | Purpose |
|------|-------|-----|-----|---------|---------|
| pve-node-1 | HP ProDesk 400 G5 Desktop Mini | Intel Core i3 | 16 GB RAM | 256 GB SSD | CasaOS / Docker |
| pve-node-2 | Lenovo Thinkcentre M265q | AMD A59120 CPU | 16 GB RAM | 256 GB SSD | Infrastructure Services |
| pve-node-3 | Intel NUC7i5BNK | Intel Core i5 | 8 GB | 2 TB SSD | Storage / Future Kubernetes |

---

## Node Details

### pve-node-1

**Hostname**
- pve-node-1

**Hardware**
- HP ProDesk 400 G5 Desktop Mini
- Intel Core i3
- 16 GB RAM
- 256 GB SSD

**Current Services**
- CasaOS
- Jellyfin
- Crafty Controller
- Portainer
- Other Docker containers

---

### pve-node-2

**Hostname**
- pve-node-2

**Hardware**
- Lenovo Thinkcentre M265q
- AMD A59120 CPU
- 16 GB RAM
- 256 GB SSD

**Current Services**
- Pi-hole
- Nginx Proxy Manager
- Syncthing

---

### pve-node-3

**Hostname**
- pve-node-3

**Hardware**
- Intel NUC7i5BNK
- Intel Core i5
- 8 GB RAM
- 2 TB SSD

**Current Services**
- NFS Share

**Planned Purpose**
- Kubernetes Worker
- NFS Storage
