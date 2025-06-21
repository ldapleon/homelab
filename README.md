# 🏠 Homelab

# Introduction

This repo contains all of the configuration and documentation of my homelab.

The purpose of my homelab is to learn and to have fun. 

Since I startet tinkering with different Linux distributions like Debian, Ubuntu, Fedora, Alpine and Alma in a Virtualbox environment on my local Windows machine, I decided to get refurbished mini-PC's to built a bare-metal homelab in my appartment. First I startet out with a Proxmox cluster where I ran multiple services like Pi-hole, Portainer, Jenkins, Nginx Proxy Manager or Vaultwarden on VMs and LXC-containers.
After running that for a few months I deciced to start over and spin up a local Kubernetes cluster. I installed the two mini-PC's with a Talos Linux standard OS.  


## Hardware

At the moment my cluster consists of the following components:

HP Prodesk 400 G3 mini (i3 CPU, 16 GB RAM, 256 SSD) | Control plane

Lenovo ThinkCentre M265q (amd A59120 CPU, 16 GB RAM, 256 SSD) | Worker node


## Software

As mentioned before, the whole K8s-cluster runs on Talos Linux OS.
The way Talos Linux works is it takes control over the entire disk it is installed on and just exposes an API you can interact with via the Talos CLI.
The config file contains all the necessary information about the clusters nodes as well as a TLS-certificate to ensure secure a connection.
As long as you have the config file of your cluster locally available, you can interact with the cluster via the CLI.

