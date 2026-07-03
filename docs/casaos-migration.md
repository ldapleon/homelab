# CasaOS Migration Plan

## Objective

Reduce the size of the CasaOS LXC root filesystem and prepare the host for Kubernetes worker nodes.

## Current State

- RootFS: 216 GB
- Actual usage: ~16 GB
- Jellyfin media stored on NFS
- Docker application data stored in /DATA/AppData

## Migration Steps

1. Create verified vzdump backup
2. Export Docker configuration (optional)
3. Remove old LXC
4. Create new LXC (50 GB RootFS)
5. Restore backup
6. Verify all services
7. Free storage for Talos worker node

## Success Criteria

- Jellyfin works
- Crafty works
- Portainer works
- Free space available on pve-node-1