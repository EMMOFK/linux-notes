# TrueNAS Home Lab Infrastructure

---

# Overview

## Purpose

This server is the primary infrastructure platform for my home lab.

It provides:

- Centralized network storage
- Media streaming
- Photo management
- Self-hosted applications
- Docker workloads
- Virtual machine hosting
- Backup and disaster recovery
- A production-like environment for learning Linux, networking, virtualization, storage, and enterprise infrastructure

---

# Environment Status

| Item | Value |
|------|------|
| Environment | Production |
| Hostname | TrueNAS |
| Operating System | TrueNAS SCALE Community Edition |
| IP Address | 192.168.68.64 |
| Remote Access | Tailscale |

---

# Infrastructure Summary

## Physical Server

| Component | Value |
|----------|------|
| Manufacturer | Dell |
| Model | Pro Max Slim FCS1250 |
| Purpose | Primary Home Lab Server |

---

## Processor

| Component | Value |
|----------|------|
| CPU | Intel Core Ultra 5 |
| Hardware Transcoding | Intel Quick Sync Video |
| Virtualization | Intel VT-x |
| IOMMU | Intel VT-d |



---

## Memory

| Component | Value |
|----------|------|
| Installed RAM | 64 GB |
| ECC | No |

---

## Storage

### Boot Device

| Device | Purpose |
|---------|---------|
| Samsung 990 Pro 2TB NVMe | TrueNAS operating system, applications and boot pool |

### Main Storage Pool

| Component | Value |
|----------|------|
| Pool | TerraMasterD4320 |
| Filesystem | ZFS |
| RAID | RAIDZ1 |
| Drives | 4 × WD Red 2TB |
| Usable Capacity | ~5.15 TiB |

---

# Dataset Layout

```text
TerraMasterD4320
├── Applications
├── Books
├── Immich
├── Media
│   └── Tdarr_Transcode
└── VMs
```

---

# SMB Shares

| Share | Purpose |
|------|---------|
| media | Movies/TV Shows & Photos|
| VMs | Virtual Machine Storage |

---

# Virtual Infrastructure

## Virtual Machines

| VM | Purpose |
|----|---------|
| Ubuntu Server | Docker Host for BookStack ecosystem |

---

# Hosted Services

This server hosts the primary media stack.

Detailed ports and URLs are documented in:

**→ Services-and-Ports.md**

---

# Storage Protection

## Snapshot Policy

### Media

- Weekly
- Retention: 4 weeks

Manual baseline snapshot:

```
post-tdarr-optimized-2026-08-04
```

### Immich

- Daily
- Retention: 2 weeks

---

# Current Storage

| Metric | Value |
|--------|------|
| Pool Capacity | ~5.15 TiB |
| Used | ~2.3 TiB |
| Available | ~2.85 TiB |

---

# Disaster Recovery Priority

| Priority | Service |
|----------|---------|
| 🔴 Critical | TrueNAS Configuration |
| 🔴 Critical | Ubuntu BookStack VM |
| 🔴 Critical | Immich |
| 🔴 Critical | BookStack |
| 🟠 High | Docker Configurations |
| 🟠 High | ARR Configuration |
| 🟡 Medium | Plex Metadata |
| 🟢 Low | Movies & TV |

---

# Recent Infrastructure Improvements


### Tdarr Optimization

- Completed successfully
- 829 successful transcodes
- Approximately 1.25 TiB of media optimized
- Converted legacy codecs to HEVC where appropriate

### Snapshot Cleanup

- Removed 74 obsolete ZFS snapshots
- Recovered approximately 2 TiB of snapshot references
- Pool utilization reduced from approximately 90% to 45%
- Created a new baseline snapshot after optimization

---

# Related Documentation

## Infrastructure

- Hardware-Inventory.md
- Ubuntu-BookStack-VM.md
- Network-Diagram.md
- Services-and-Ports.md

## Applications

- Plex.md
- Tdarr.md
- Immich.md
- ARR-Stack.md
- BookStack.md

## Disaster Recovery

- TrueNAS-Recovery.md
- Ubuntu-VM-Recovery.md
- Backup-Strategy.md