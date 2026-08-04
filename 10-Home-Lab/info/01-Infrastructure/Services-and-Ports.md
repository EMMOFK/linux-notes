# Services and Ports

---

# Overview

This document provides a complete inventory of all services running within the home lab environment.

It serves as a quick reference for:

- Web interfaces
- Service locations
- Default ports
- Host systems
- Administrative access

---

# Network Overview

| Device | IP Address | Purpose |
|---------|------------|---------|
| TrueNAS SCALE | 192.168.68.64 | Storage server and application host |
| Ubuntu BookStack VM | 192.168.68.59 | Docker host for book services |

---

# Core Infrastructure

| Service | Host | Port | URL | Purpose |
|---------|------|------|-----|---------|
| TrueNAS Web UI | TrueNAS | 80 | http://192.168.68.64 | TrueNAS administration |
| Tailscale | TrueNAS | N/A | Installed client | Secure remote access |

---

# Media Stack (TrueNAS)

| Service | Port | URL | Purpose |
|---------|-----:|-----|---------|
| Plex | 32400 | http://192.168.68.64:32400 | Media streaming server |
| Tdarr | 30088 | http://192.168.68.64:30088 | Automatic media transcoding |
| Overseerr | 30002 | http://192.168.68.64:30002 | Media request management |
| Radarr | 30025 | http://192.168.68.64:30025 | Movie management |
| Sonarr | 30113 | http://192.168.68.64:30113 | TV show management |
| Prowlarr | 30050 | http://192.168.68.64:30050 | Indexer management |
| SABnzbd | 30055 | http://192.168.68.64:30055 | Usenet downloader |
| qBittorrent | 30024 | http://192.168.68.64:30024 | Torrent downloader |
| Clonarr | 30427 | http://192.168.68.64:30427 | ARR configuration backup |

---

# Self-Hosted Services (TrueNAS)

| Service | Port | URL | Purpose |
|---------|-----:|-----|---------|
| Immich | 30041 | http://192.168.68.64:30041 | Photo management |
| Homarr | 30100 | http://192.168.68.64:30100 | Home lab dashboard |

---

# Book Server (Ubuntu VM)

Host:

**Ubuntu Server VM**

IP Address:

**192.168.68.59**

| Service | Port | URL | Purpose |
|---------|-----:|-----|---------|
| BookStack | 6875 | http://192.168.68.59:6875 | Documentation wiki |
| Readarr | 8787 | http://192.168.68.59:8787 | Book management |
| Prowlarr | 9696 | http://192.168.68.59:9696 | Book indexers |
| SABnzbd | 8080 | http://192.168.68.59:8080 | Book downloads |
| Calibre-Web | 8083 | http://192.168.68.59:8083 | eBook library |

---

# Service Groups

## TrueNAS Services

- TrueNAS
- Plex
- Tdarr
- Immich
- Homarr
- Overseerr
- Radarr
- Sonarr
- Prowlarr
- SABnzbd
- qBittorrent
- Clonarr
- Tailscale

---

## Ubuntu VM Services

- BookStack
- Readarr
- Prowlarr
- SABnzbd
- Calibre-Web

---

# Notes

## TrueNAS

Hosts:

- Storage
- Media services
- Photo management
- Dashboard
- ARR media stack
- Virtual machines

---

## Ubuntu VM

Dedicated Docker host for the self-hosted book ecosystem.

Services are intentionally separated from the media stack to simplify maintenance and future expansion.

---

# Future Improvements

Planned additions include:

- HTTPS with a reverse proxy
- Internal DNS names (e.g. `plex.home`, `bookstack.home`)
- AdGuard Home as the primary DNS server
- Monitoring of all services through Prometheus and Grafana
- Centralized authentication for self-hosted services

---

# Last Updated

August 2026