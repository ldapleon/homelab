## Current Storage Layout

| Host | Storage | Current Usage |
|------|---------|---------------|
| pve-node-3 | 2 TB SSD | Proxmox, NFS share, media storage |

---

## Current NFS Setup

The NFS server is currently running directly on `pve-node-3`.

It is used by Jellyfin for media streaming.

```text
pve-node-3
└── 2 TB SSD
    └── NFS Share
        └── Jellyfin Media Library