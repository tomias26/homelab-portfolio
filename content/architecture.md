---
title: "Network Architecture & Topology"
description: "Multi-VLAN network design and traffic isolation overview."
---

## Executive Overview

This network architecture is built around **defense-in-depth**, **traffic isolation**, and **zero-trust access**. Rather than operating on a flat home network, all devices and services are segmented into dedicated Virtual LANs (VLANs) with strict firewall rules controlling inter-VLAN routing.

---

## Subnet & VLAN Breakdown

| VLAN ID | Subnet Name | Purpose & Security Stance |
| :--- | :--- | :--- |
| **VLAN 10** | Management | Admin interfaces, switches, IPMI |
| **VLAN 20** | Servers & Core | Host OS, Docker containers, reverse proxy |
| **VLAN 30** | Security Cameras | **No WAN Access**; isolated feeds to Frigate NVR |
| **VLAN 40** | IoT & Smart Home | Restricted access; Home Assistant integrations |
| **VLAN 50** | Trusted LAN | Primary desktop/workstation access |

---

## Security Policies & Isolation

1. **Surveillance Isolation:** IP cameras on VLAN 30 are completely blocked from accessing the public internet. Communication is restricted strictly to the local NVR host on VLAN 20.
2. **Reverse Proxy & Remote Access:** Inbound requests are handled via secure mesh tunnels (Tailscale/Cloudflare) routing directly to local proxy endpoints, avoiding open port exposures on the public WAN IP.
