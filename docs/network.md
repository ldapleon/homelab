# Current Network

This section documents the current production network.


| Hostname      | IP Address       | Purpose              |
|---------------|------------------|----------------------|
| pve-node-1    | 192.168.188.104  | Proxmox Host         |
| pve-node-2    | 192.168.188.88   | Proxmox Host         |
| pve-node-3    | 192.168.188.163  | Proxmox Host         |
| ct-pihole     | 192.168.188.53   | DNS                  |
| ct-casaos     | 192.168.188.158  | Docker Host          |
| ct-homepage   | 192.168.188.162  | Homepage Dashboard   |
| ct-syncthing  | 192.168.188.165  | File Synchronization |



## Planned Kubernetes Nodes

| Name | IP Address | Status |
|------|------------|--------|
| talos-cp-1 | 192.168.188.69 | Planned |
| talos-worker-1 | TBD | Planned |
| talos-worker-2 | TBD | Planned |



# DNS-Architektur im Homelab

## Ziel

Das Homelab verwendet Pi-hole als zentralen DNS-Server für das Heimnetz und Unbound als rekursiven DNS-Resolver.

Dadurch werden folgende Ziele erreicht:

- lokale DNS-Namen wie `vaultwarden.home.arpa`, `pihole.home.arpa`, `longhorn.home.arpa`
- Werbe- und Tracking-Filterung über Pi-hole
- rekursive DNS-Auflösung über Unbound
- DNSSEC-Validierung
- weniger Abhängigkeit von externen DNS-Anbietern wie Cloudflare, Google oder Quad9

---

## Architektur

```text
Clients
  ↓
FRITZ!Box / DHCP
  ↓
Pi-hole
  ↓
Unbound
  ↓
Root DNS Server
  ↓
TLD DNS Server
  ↓
Authoritative DNS Server