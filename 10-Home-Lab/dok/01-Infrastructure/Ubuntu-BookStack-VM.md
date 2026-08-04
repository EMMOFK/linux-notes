# Ubuntu BookStack VM

---

# Overview

This virtual machine provides a dedicated Linux environment for self-hosted documentation and book management services.

Separating these workloads from the TrueNAS host provides several benefits:

- Independent operating system
- Simplified maintenance
- Easier Docker management
- Isolation from storage services
- Better disaster recovery
- Hands-on Linux administration experience

The VM acts as a dedicated Docker host for documentation and ebook management.

---

# System Information

| Item | Value |
|------|-------|
| Operating System | Ubuntu Server |
| Virtualization Platform | TrueNAS SCALE |
| Host Server | TrueNAS |
| Purpose | Docker Host |
| Status | Production |
| IP Address | 192.168.68.59 |

---

# Purpose

This virtual machine hosts services related to:

- Documentation
- Book management
- Ebook library
- Usenet downloads
- Index management

Keeping these services isolated from the media stack improves maintainability and reduces the impact of software updates.

---

# Storage

The virtual machine disk is stored on the **fast-pool** NVMe SSD.

Benefits include:

- Faster boot times
- Faster Docker startup
- Lower latency
- Improved database performance
- Better responsiveness than HDD storage

Storage Pool

```
fast-pool
```

Underlying Storage

```
Samsung 990 PRO 2 TB NVMe
```

---

# Hosted Services

| Service | URL | Purpose |
|----------|-----|----------|
| BookStack | http://192.168.68.59:6875 | Documentation Wiki |
| Readarr | http://192.168.68.59:8787 | Ebook Management |
| Prowlarr | http://192.168.68.59:9696 | Index Manager |
| SABnzbd | http://192.168.68.59:8080 | Usenet Downloader |
| Calibre-Web | http://192.168.68.59:8083 | Ebook Library |

---

# Docker Environment

The VM functions as a dedicated Docker server.

Current containers include:

- BookStack
- Readarr
- Prowlarr
- SABnzbd
- Calibre-Web

Advantages:

- Simple container updates
- Easy backups
- Independent restart capability
- Reduced load on the TrueNAS host

---

# Networking

LAN Address

```
192.168.68.59
```

Accessible from:

- Desktop PC
- Linux Laptop
- Other LAN devices
- Tailscale (when enabled)

Communication with TrueNAS:

- Reads media from SMB shares
- Downloads stored on TrueNAS datasets
- Book library stored on shared storage

---

# Integration with TrueNAS

The Ubuntu VM works alongside the TrueNAS host.

Responsibilities:

TrueNAS

- Storage
- ZFS
- Snapshots
- SMB
- Media stack

Ubuntu VM

- Documentation
- Ebook management
- Docker services
- Linux workloads

This separation keeps infrastructure modular and easier to maintain.

---

# Backup Strategy

Critical Data

- Docker volumes
- BookStack database
- BookStack uploads
- Readarr configuration
- Prowlarr configuration
- SABnzbd configuration
- Calibre-Web configuration

Recovery Process

1. Restore the Ubuntu VM.
2. Install Docker.
3. Restore Docker volumes.
4. Restore application configurations.
5. Verify network connectivity.
6. Confirm access to TrueNAS SMB shares.

---

# Disaster Recovery Priority

| Priority | Component |
|----------|-----------|
| 🔴 Critical | BookStack |
| 🔴 Critical | Docker volumes |
| 🔴 Critical | Application configurations |
| 🟠 High | Readarr |
| 🟠 High | Prowlarr |
| 🟠 High | Calibre-Web |
| 🟢 Low | Download cache |

---

# Future Improvements

Planned enhancements include:

- Docker Compose stored in Git
- Automated configuration backups
- Scheduled VM backups
- Tailscale remote administration
- Monitoring with Prometheus and Grafana
- Automated disaster recovery documentation

---

# Design Philosophy

This virtual machine follows several enterprise design principles:

- Separate storage from applications.
- Separate infrastructure roles.
- Keep documentation isolated.
- Use Docker for service portability.
- Store virtual machines on high-performance SSD storage.
- Design for straightforward recovery after failure.