# Storage Architecture

---

# Overview

This document describes the storage architecture of the TrueNAS home lab server.

The server is designed using multiple ZFS storage pools, with each pool dedicated to a specific workload. Separating the operating system, high-performance workloads, and bulk storage improves performance, simplifies administration, and reduces the impact of failures.

The architecture follows the same storage-tiering concepts commonly used in enterprise environments.

---

# Storage Design Goals

The storage platform was designed with the following objectives:

- Separate the operating system from user data.
- Run applications from fast NVMe storage.
- Keep media storage isolated from application workloads.
- Protect important data using ZFS snapshots.
- Simplify disaster recovery.
- Allow future hardware upgrades with minimal downtime.

---

# Storage Tiering Strategy

The server is divided into three storage tiers.

| Tier | Pool | Purpose |
|------|------|---------|
| Operating System | boot-pool | TrueNAS operating system |
| Performance Tier | fast-pool | Applications, virtual machines and high-speed workloads |
| Capacity Tier | TerraMasterD4320 | Long-term media and user data |

This separation ensures that application performance is not affected by large media transfers or disk-intensive workloads.

---

# Storage Pools

| Pool | Purpose | Physical Device |
|------|---------|----------------|
| boot-pool | TrueNAS SCALE operating system | SanDisk 256 GB SSD |
| fast-pool | High-performance SSD storage | Samsung 990 PRO 2 TB NVMe |
| TerraMasterD4320 | Bulk storage | TerraMaster D4-320 (4 × 2 TB WD drives) |

---

# boot-pool

## Purpose

The boot pool is dedicated exclusively to the operating system.

It stores:

- TrueNAS SCALE
- Boot environments
- System configuration
- System updates

### Device

| Component | Value |
|----------|------|
| SSD | SanDisk SD8SB8U-256G |
| Capacity | 256 GB |

Keeping the operating system isolated allows TrueNAS to be reinstalled without affecting application or media data.

---

# fast-pool

## Purpose

The fast-pool provides high-speed NVMe storage for performance-sensitive workloads.

Current workloads include:

- Ubuntu BookStack Virtual Machine
- TrueNAS application storage
- Docker workloads
- Future virtual machines
- Future databases

### Device

| Component | Value |
|----------|------|
| SSD | Samsung 990 PRO |
| Capacity | 2 TB |
| Interface | PCIe NVMe |

### Current Architecture

```
fast-pool
│
├── Ubuntu BookStack VM
├── TrueNAS Applications
├── Docker Containers
├── Future Virtual Machines
└── High-speed datasets
```

### Advantages

- Extremely low latency
- High IOPS
- Fast virtual machine performance
- Faster application startup
- Reduced HDD contention
- Excellent Docker performance

---

# TerraMasterD4320

## Purpose

The TerraMaster D4-320 provides high-capacity storage for long-term data.

Current workloads include:

- Movies
- TV Shows
- Books
- Immich Library
- SMB Shares
- User data
- Tdarr working directories

Unlike the fast-pool, this storage is optimized for capacity rather than performance.

---

## Physical Layout

| Bay | Device | Model | RPM |
|-----|--------|-------|----:|
| Bay 1 | /dev/sdb | WD20EFRX-68EUZN0 | 5400 |
| Bay 2 | /dev/sdc | WD20EFRX-68EUZN0 | 5400 |
| Bay 3 | /dev/sdd | WD2001FFSX-68JNUN0 | 7200 |
| Bay 4 | /dev/sde | WD2001FFSX-68JNUN0 | 7200 |

---

## RAID Layout

Filesystem

```
ZFS
```

Layout

```
RAIDZ1
```

### Why RAIDZ1?

RAIDZ1 was selected because it provides:

- Protection against a single drive failure
- Better storage efficiency than mirrored vdevs
- Suitable redundancy for a home media server
- Straightforward migration to larger disks over time

---

# Dataset Layout

```
TerraMasterD4320
├── Applications
├── Books
├── Immich
├── Media
│   ├── Movies
│   ├── TV Shows
│   └── Tdarr_Transcode
└── VMs
```

> **Note**
>
> The Ubuntu BookStack VM currently resides on the **fast-pool** to maximise virtual machine performance. The `VMs` dataset on `TerraMasterD4320` is retained for future use or archival workloads.

---

# Snapshot Strategy

## Media

| Setting | Value |
|----------|------|
| Frequency | Weekly |
| Retention | 4 Weeks |

Purpose:

Protect against accidental deletion while keeping snapshot storage under control.

Current baseline snapshot

```
post-tdarr-optimized-2026-08-04
```

---

## Immich

| Setting | Value |
|----------|------|
| Frequency | Daily |
| Retention | 2 Weeks |

Reason:

Photos change much more frequently than media files and therefore require more frequent recovery points.

---

# Storage Optimisation

## Tdarr

The media library is automatically optimised using Tdarr.

Benefits

- Converts H.264 to HEVC
- Preserves subtitles
- Preserves preferred audio tracks
- Reduces storage consumption

Results

- 829 successful transcodes
- Approximately 1.25 TiB reclaimed

---

# Performance Considerations

The storage architecture separates high-speed workloads from bulk storage.

Benefits include:

- Ubuntu BookStack VM runs entirely from NVMe storage.
- Applications remain responsive while media is being read or written.
- Docker containers are isolated from HDD latency.
- Large Plex streams do not affect virtual machine performance.
- Future databases can remain on SSD storage.

---

# Disaster Recovery

If the operating system fails:

1. Reinstall TrueNAS SCALE.
2. Import all ZFS pools.
3. Restore the exported TrueNAS configuration.
4. Verify networking.
5. Verify applications.
6. Verify virtual machines.

Because user data resides on separate pools, reinstalling the operating system does not affect stored media or application data.

---

# Future Improvements

## Planned

- Upgrade the storage pool to larger capacity drives.
- Upgrade networking to 2.5 GbE or faster.
- Integrate the APC BX1200MI UPS with TrueNAS.
- Automate configuration backups.
- Implement off-site backups.

---

# Design Philosophy

The storage architecture follows enterprise storage principles:

- Separate operating system from user data.
- Separate performance workloads from capacity workloads.
- Protect critical datasets with snapshots.
- Optimise applications using NVMe storage.
- Keep media storage scalable and easily recoverable.
- Design for future expansion with minimal disruption.