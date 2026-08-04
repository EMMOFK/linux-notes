# Network Diagram

---

# Overview

This document describes the logical network layout of the home lab.

The network uses the `192.168.68.0/22` subnet, with the TP-Link Deco system providing the default gateway and DHCP services.

---

# Core Network

```text
                              Internet
                                  │
                                  ▼
                         TP-Link Deco Router
                           192.168.68.1
                    Default Gateway / DHCP / DNS
                                  │
                                  │
                    LAN: 192.168.68.0/22
                                  │
          ┌───────────────────────┼────────────────────────┐
          │                       │                        │
          ▼                       ▼                        ▼
   TrueNAS Server          Linux Laptop             Other LAN Devices
   192.168.68.64           192.168.68.69            Phones / TVs / PCs
          │
          │
          └────────────── Hosts Ubuntu VM
                           192.168.68.59
```

---

# TrueNAS Service Layout

```text
TrueNAS SCALE
192.168.68.64
│
├── TrueNAS Web UI
│   └── Port 80
│
├── Plex
│   └── Port 32400
│
├── Immich
│   └── Port 30041
│
├── Homarr
│   └── Port 30100
│
├── Tdarr
│   └── Port 30088
│
├── Clonarr
│   └── Port 30427
│
├── Overseerr
│   └── Port 30002
│
├── qBittorrent
│   └── Port 30024
│
├── Radarr
│   └── Port 30025
│
├── Sonarr
│   └── Port 30113
│
├── Prowlarr
│   └── Port 30050
│
├── SABnzbd
│   └── Port 30055
│
├── AdGuard Home
│   ├── Web UI: Port 30004
│   └── DNS: Port 53
│
├── Prometheus
│
├── FlareSolverr
│
└── Tailscale
```

---

# Ubuntu BookStack VM

```text
Ubuntu Server VM
192.168.68.59
│
├── BookStack
│   └── Port 6875
│
├── Readarr
│   └── Port 8787
│
├── Prowlarr
│   └── Port 9696
│
├── SABnzbd
│   └── Port 8080
│
└── Calibre-Web
    └── Port 8083
```

---

# Application Dependencies

```text
                         Overseerr
                             │
                             ▼
                           Radarr
                             │
                             ├──────────► Prowlarr
                             │
                             ├──────────► SABnzbd
                             │
                             └──────────► qBittorrent


                         Overseerr
                             │
                             ▼
                           Sonarr
                             │
                             ├──────────► Prowlarr
                             │
                             ├──────────► SABnzbd
                             │
                             └──────────► qBittorrent


                           Plex
                             │
                             ▼
                  TerraMasterD4320/Media
                             │
                             ▼
                           Tdarr
```

---

# Book Services Dependencies

```text
                         Readarr
                            │
                            ├──────────► Prowlarr
                            │
                            └──────────► SABnzbd
                            │
                            ▼
                         Books Library
                            │
                            ▼
                       Calibre-Web
```

---

# Storage Connectivity

```text
TrueNAS Server
192.168.68.64
│
├── boot-pool
│   └── SanDisk 256 GB SSD
│
├── fast-pool
│   └── Samsung 990 PRO 2 TB NVMe
│       └── Ubuntu BookStack VM
│
└── TerraMasterD4320
    └── RAIDZ1: 4 × 2 TB HDD
        ├── Media
        ├── Books
        ├── Immich
        ├── Applications
        │   └── Prometheus data
        └── SMB shares
```

---

# Remote Access

Remote access is provided using Tailscale.

```text
Remote Device
      │
      ▼
Tailscale Network
      │
      ▼
TrueNAS Server
192.168.68.64
      │
      └── Internal services and Ubuntu VM
```

Tailscale provides encrypted access without exposing the individual application ports directly to the public Internet.

---

# Address Summary

| Device | IP Address | Purpose |
|--------|------------|---------|
| TP-Link Deco | 192.168.68.1 | Gateway, DHCP and current DNS |
| Ubuntu BookStack VM | 192.168.68.59 | Docker host for book services |
| TrueNAS | 192.168.68.64 | Storage, applications and virtualization |
| Linux Laptop | 192.168.68.69 | Administration workstation |

---

# Network Notes

- LAN subnet: `192.168.68.0/22`
- Default gateway: `192.168.68.1`
- TrueNAS uses a reserved or static address.
- The Ubuntu VM uses a fixed address.
- Most application interfaces are currently available over unencrypted HTTP on the trusted LAN.
- Tailscale is used for remote access.
- AdGuard Home is installed, but the TP-Link Deco remains documented as the current DNS service until client DNS settings are confirmed.
- VLANs are not currently implemented.

---

# Future Improvements

- Confirm AdGuard Home as the primary LAN DNS resolver.
- Document DHCP reservations.
- Add a managed switch.
- Introduce VLANs for servers, clients, IoT devices and guests.
- Upgrade the LAN to 2.5 GbE.
- Add internal DNS names for services.
- Introduce HTTPS using a reverse proxy.
- Restrict management interfaces to trusted administrator devices.