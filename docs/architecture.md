                        Internet
                            │
                       Fritz!Box
                            │
                    192.168.188.0/24
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
    pve-node-1         pve-node-2       pve-node-3
          │                 │                 │
      CasaOS LXC       Pi-hole LXC      NFS Server
          │            NPM LXC          (on Proxmox)
          │            Syncthing LXC
          │
      Docker
      ├── Jellyfin
      ├── Crafty
      ├── Portainer
      └── ...