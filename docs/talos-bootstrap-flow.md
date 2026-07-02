# Talos Bootstrap Flow

## Purpose

This document explains how a Talos Kubernetes cluster is bootstrapped.

---

## Step 1 – Boot Talos ISO

The VM boots from the Talos ISO.

At this point, Talos is running in memory and waits for a machine configuration.

---

## Step 2 – Talos API becomes available

Talos does not use SSH.

Management is done through the Talos API using `talosctl`.

---

## Step 3 – Generate Machine Configs

Machine configuration files are generated for:

- Control plane nodes
- Worker nodes

These configs define how each node should behave.

---

## Step 4 – Apply Machine Config

The configuration is applied to each node.

After that, Talos installs itself to disk and reboots.

---

## Step 5 – Bootstrap etcd

The first control plane node initializes `etcd`.

`etcd` stores the state of the Kubernetes cluster.

---

## Step 6 – Kubernetes Control Plane starts

After `etcd` is ready, Kubernetes control plane components start.

This includes:

- kube-apiserver
- kube-controller-manager
- kube-scheduler

---

## Step 7 – Worker Nodes join

Worker nodes receive their configuration and join the cluster.

---

## Step 8 – Retrieve kubeconfig

The Kubernetes config is retrieved using `talosctl`.

After this step, the cluster can be managed with `kubectl`.

---

## Step 9 – Install CNI

A CNI plugin is required before pods can communicate.

This cluster will use Cilium.

---

## Step 10 – Install Core Infrastructure

After the cluster is ready, the following components will be installed:

- Cilium
- MetalLB
- Traefik
- cert-manager
- Flux CD
- NFS CSI Driver

---

## Lessons Learned

- Talos is managed through an API, not SSH.
- MachineConfigs define the desired state of each node.
- `etcd` is the database of the Kubernetes cluster.
- A CNI is required before the cluster is fully usable.