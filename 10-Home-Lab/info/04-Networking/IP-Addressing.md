# IP Addressing

---

# Overview

This document defines the IP addressing scheme used throughout the home lab.

Maintaining a documented addressing plan simplifies:

- Troubleshooting
- Disaster recovery
- Service discovery
- Network expansion
- Static IP management
- DNS configuration

The network is intentionally designed so that all infrastructure devices use static IP addresses while client devices continue to use DHCP.

---

# Network Information

| Setting | Value |
|---------|------|
| Network Address | 192.168.68.0/22 |
| Subnet Mask | 255.255.252.0 |
| Gateway | 192.168.68.1 |
| DHCP Server | TP-Link Deco |
| Current DNS | TP-Link Deco |
| Future DNS | AdGuard Home |
| Remote Access | Tailscale VPN |

---

# Network Range

```
Network:
192.168.68.0/22

Usable Range:
192.168.68.1
↓

192.168.71.254
```

This provides approximately **1,022 usable IP addresses**, allowing significant room for future expansion.

---

# Addressing Strategy

The home lab uses the following principles:

- Infrastructure uses static IP addresses.
- User devices obtain addresses via DHCP.
- Servers retain fixed addresses to ensure consistent access.
- Services are documented using IP addresses rather than relying solely on hostnames.
- Future infrastructure should follow the existing allocation scheme.

---

# Static Infrastructure

## TrueNAS SCALE

| Property | Value |
|----------|------|
| Hostname | TrueNAS |
| IP Address | 192.168.68.64 |
| Purpose | Primary Storage Server |

---

## Ubuntu Server VM

| Property | Value |
|----------|------|
| Hostname | Ubuntu BookStack VM |
| IP Address | 192.168.68.59 |
| Purpose | Docker Host |

---

# Infrastructure Services

## TrueNAS Services

| Service | Port | URL |
|----------|-----:|-----|
| TrueNAS Web UI | 80 | http://192.168.68.64 |
| Plex | 32400 | http://192.168.68.64:32400 |
| Immich | 30041 | http://192.168.68.64:30041 |
| Homarr | 30100 | http://192.168.68.64:30100 |
| Tdarr | 30088 | http://192.168.68.64:30088 |
| Clonarr | 30427 | http://192.168.68.64:30427 |
| Overseerr | 30002 | http://192.168.68.64:30002 |
| qBittorrent | 30024 | http://192.168.68.64:30024 |
| Radarr | 30025 | http://192.168.68.64:30025 |
| Sonarr | 30113 | http://192.168.68.64:30113 |
| Prowlarr | 30050 | http://192.168.68.64:30050 |
| SABnzbd | 30055 | http://192.168.68.64:30055 |

---

## Ubuntu VM Services

| Service | Port | URL |
|----------|-----:|-----|
| BookStack | 6875 | http://192.168.68.59:6875 |
| Readarr | 8787 | http://192.168.68.59:8787 |
| Prowlarr | 9696 | http://192.168.68.59:9696 |
| SABnzbd | 8080 | http://192.168.68.59:8080 |
| Calibre-Web | 8083 | http://192.168.68.59:8083 |

---

# DHCP Strategy

The TP-Link Deco router currently provides DHCP services for client devices.

Infrastructure systems are assigned static IP addresses to ensure:

- Reliable remote administration
- Consistent service endpoints
- Stable documentation
- Predictable network behaviour

---

# Address Allocation Plan

| Range | Purpose |
|---------|---------|
| 192.168.68.1 | Gateway |
| 192.168.68.2 - 192.168.68.49 | Reserved for future infrastructure |
| 192.168.68.50 - 192.168.68.99 | Servers and Virtual Machines |
| 192.168.68.100 - 192.168.71.254 | DHCP Clients |

---

# Remote Access

Remote administration is provided using Tailscale.

External devices connect securely through an encrypted WireGuard tunnel without exposing management interfaces to the public Internet.

Remote administration includes:

- TrueNAS
- Ubuntu VM
- SSH
- Web applications
- SMB access (when required)

---

# Future Address Plan

The following address ranges are reserved for future expansion.

| Planned Device | Reserved |
|----------------|----------|
| Additional Virtual Machines | Yes |
| Monitoring Server | Yes |
| Reverse Proxy | Yes |
| AdGuard Home DNS | Yes |
| Enterprise Firewall | Yes |
| Network Controller | Yes |

---

# Design Philosophy

The IP addressing scheme follows enterprise networking principles:

- Static addressing for infrastructure.
- Dynamic addressing for clients.
- Consistent documentation.
- Logical address allocation.
- Capacity for future growth.
- Simplified disaster recovery and troubleshooting.

---

# Related Documentation

- Network Diagram
- Services and Ports
- DNS
- Tailscale
- SMB and File Shares
- TrueNAS Infrastructure