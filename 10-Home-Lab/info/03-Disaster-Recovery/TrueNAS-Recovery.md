# TrueNAS Recovery

---

# Overview

This document describes the complete recovery procedure for rebuilding the TrueNAS home lab server following catastrophic hardware failure, operating system corruption, or boot device replacement.

The objective is to restore all storage pools, services, networking, applications, and virtual machines while minimizing downtime and data loss.

---

# Recovery Decision Tree

Server won't boot?
        │
        ▼
Boot drive failed?
        │
 ┌──────┴──────┐
 │             │
Yes           No
 │             │
Reinstall    Import Config
TrueNAS
 │
 ▼
Import Pools
 │
 ▼
Restore Apps
 │
 ▼
Verify VM
 │
 ▼
Production

---

# Recovery Objectives

The recovery procedure should restore:

- TrueNAS SCALE operating system
- Network configuration
- ZFS storage pools
- Snapshots
- Applications
- Virtual machines
- SMB shares
- User accounts
- Scheduled tasks

---

# Current Infrastructure

| Component | Value |
|-----------|-------|
| Hostname | TrueNAS |
| Operating System | TrueNAS SCALE Community Edition |
| LAN Address | 192.168.68.64 |
| Gateway | 192.168.68.1 |
| Remote Access | Tailscale |

---

# Storage Pools

| Pool | Purpose |
|------|---------|
| boot-pool | TrueNAS operating system |
| fast-pool | Applications, containers and VM storage |
| TerraMasterD4320 | Media, Books, Immich, SMB shares |

---

# Recovery Requirements

Before beginning recovery, ensure the following are available:

- Latest TrueNAS SCALE installer
- Latest exported TrueNAS configuration
- Administrator credentials
- Internet connection
- GitHub documentation repository
- Ubuntu VM backup (if applicable)

---

# Recovery Procedure

## Step 1 — Install TrueNAS

Install the latest supported version of TrueNAS SCALE.

Do not create any storage pools during installation.

---

## Step 2 — Configure Networking

Configure:

- Hostname
- Static IP address
- Gateway
- DNS

Expected configuration:

| Setting | Value |
|----------|------|
| Hostname | TrueNAS |
| IP Address | 192.168.68.64 |
| Gateway | 192.168.68.1 |

Verify network connectivity before continuing.

---

## Step 3 — Restore Configuration

Import the most recent exported TrueNAS configuration database.

This restores:

- Users
- Shares
- Network configuration
- Scheduled tasks
- Applications
- Permissions
- System settings

Reboot if prompted.

---

## Step 4 — Import Storage Pools

Navigate to:

Storage

↓

Import Pool

Import:

- fast-pool
- TerraMasterD4320

Do **not** create new pools if the existing ZFS pools are intact.

Verify that all datasets are present after import.

---

## Step 5 — Verify Datasets

Expected dataset layout:

```
fast-pool
├── ix-applications
└── VM Storage

TerraMasterD4320
├── Applications
├── Books
├── Immich
├── Media
│   └── Tdarr_Transcode
└── VMs
```

---

## Step 6 — Verify SMB Shares

Confirm that the following shares are available:

| Share | Purpose |
|--------|----------|
| media | Movies and TV |
| VMs | Virtual machine storage |

Verify access from client devices.

---

## Step 7 — Verify Applications

Expected applications include:

- AdGuard Home
- Clonarr
- FlareSolverr
- Homarr
- Immich
- Overseerr
- Plex
- Prometheus
- Prowlarr
- qBittorrent
- Radarr
- SABnzbd
- Sonarr
- Tailscale
- Tdarr

Confirm each application starts successfully.

---

## Step 8 — Verify Virtual Machines

Verify:

Ubuntu BookStack VM

Expected IP:

```
192.168.68.59
```

Confirm the VM boots successfully.

---

## Step 9 — Verify Network Services

Confirm access to:

| Service | URL |
|----------|-----|
| TrueNAS | http://192.168.68.64 |
| Plex | http://192.168.68.64:32400 |
| Immich | http://192.168.68.64:30041 |
| Homarr | http://192.168.68.64:30100 |
| Tdarr | http://192.168.68.64:30088 |
| Overseerr | http://192.168.68.64:30002 |
| qBittorrent | http://192.168.68.64:30024 |
| Radarr | http://192.168.68.64:30025 |
| Sonarr | http://192.168.68.64:30113 |
| Prowlarr | http://192.168.68.64:30050 |
| SABnzbd | http://192.168.68.64:30055 |

---

## Step 10 — Verify Snapshots

Expected snapshot policies:

### Media

- Weekly
- Retention: 4 Weeks

### Immich

- Daily
- Retention: 2 Weeks

Verify the manual baseline snapshot:

```
post-tdarr-optimized-2026-08-04
```

---

## Step 11 — Verify Remote Access

Confirm:

- Tailscale connected
- SSH available
- Web interface accessible

---

# Post-Recovery Checklist

Verify the following:

- TrueNAS dashboard healthy
- All pools online
- No degraded disks
- SMART tests enabled
- Scrub schedule configured
- Snapshot tasks enabled
- Applications running
- Ubuntu VM operational
- SMB shares accessible
- Documentation updated if changes were required

---

# Estimated Recovery Time

| Task | Estimated Time |
|------|----------------|
| Install TrueNAS | 15–20 minutes |
| Restore Configuration | 5 minutes |
| Import Pools | 5–10 minutes |
| Verify Applications | 15 minutes |
| Verify VM | 10 minutes |
| Final Testing | 15 minutes |

Estimated total:

**Approximately 1 hour**

---

# Recovery Philosophy

This infrastructure is designed around the following principles:

- The operating system is disposable.
- Data resides on separate ZFS pools.
- Configuration is backed up independently.
- Documentation is stored off-site in GitHub.
- Recovery should be repeatable, documented, and require minimal guesswork.

A complete server rebuild should be achievable in approximately one hour using this document and the associated infrastructure documentation.