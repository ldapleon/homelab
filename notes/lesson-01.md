# Lesson 01 - Preparing Talos

## Objective

Understand how Talos is installed and why the Talos Factory exists.

---

## What I Learned

- Talos Factory creates customized installation images.
- The ISO is used only for bootstrapping.
- Talos installs itself after receiving its MachineConfig.
- Talos is managed through an API instead of SSH.

---

## Questions

- Which system extensions will I need in the future?
- How does Talos update itself?

---

## Personal Notes

Talos has a very different philosophy than a traditional Linux server. Everything is configuration-driven, which fits well with GitOps.


## Decisions Made

- Talos Version: v1.13.5
- Installation Method: ISO
- Platform: Manual Proxmox deployment
- QEMU Guest Agent: Enabled
- iSCSI Tools: Not required at this stage

## Why?

The goal is to keep the first cluster simple, reproducible and easy to understand. Additional features and extensions can be added later when there is a real use case.