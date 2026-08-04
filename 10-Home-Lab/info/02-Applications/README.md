# Applications

---

# Overview

This section documents every application running within the home lab.

Each document explains:

- What the application does
- Why it exists
- Where it runs
- Storage requirements
- Network configuration
- Backup strategy
- Recovery procedure
- Dependencies
- Update process
- Troubleshooting

The goal is to ensure every application can be rebuilt and maintained without relying on memory.

---

# Application Groups

## Documentation

- BookStack

---

## Media Management

- Plex
- Tdarr
- Overseerr

---

## ARR Stack

- Radarr
- Sonarr
- Readarr
- Prowlarr
- SABnzbd
- qBittorrent
- Clonarr
- FlareSolverr

---

## Photos

- Immich

---

## Infrastructure

- Homarr
- AdGuard Home
- Prometheus
- Tailscale

---

# Application Architecture

```text
                         Home Lab
                              │
        ┌─────────────────────┴─────────────────────┐
        │                                           │
   TrueNAS SCALE                          Ubuntu Server VM
        │                                           │
        │                                           │
   Plex                                      BookStack
   Tdarr                                     Readarr
   Immich                                    Prowlarr
   Homarr                                    SABnzbd
   AdGuard                                   Calibre-Web
   Prometheus
   ARR Stack
```

---

# Documentation Standards

Each application document follows the same structure:

- Overview
- Purpose
- Host System
- Storage
- Network
- Dependencies
- Backup Strategy
- Recovery
- Maintenance
- Troubleshooting
- Future Improvements

Maintaining a consistent structure makes the documentation easier to navigate and maintain as the home lab grows.