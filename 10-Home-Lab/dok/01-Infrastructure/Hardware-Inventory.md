# Hardware Inventory

---

# Overview

This document records the complete hardware specification of the TrueNAS Home Lab server.

---

# System Information

| Item | Value |
|------|------|
| Hostname | TrueNAS |
| Manufacturer | Dell Inc. |
| Model | Dell Pro Max Slim FCS1250 |
| Purpose | Primary Home Lab Server |
| Operating System | TrueNAS SCALE Community Edition |

---

# Processor

| Component | Value |
|----------|------|
| CPU | Intel Core Ultra 5 235 |
| Architecture | x86_64 |
| Physical Cores | 14 |
| Threads | 14 |
| Base Frequency | 800 MHz |
| Maximum Turbo Frequency | 6.4 GHz |
| L3 Cache | 24 MB |
| Hardware Transcoding | Intel Quick Sync Video |
| Virtualization | Intel VT-x |
| IOMMU | Intel VT-d |

---

# Memory

| Component | Value |
|----------|------|
| Installed RAM | 64 GB |
| Memory Type | DDR5 |
| Installed Modules | 4 × 16 GB |
| Module Speed | 5600 MT/s |
| Configured Speed | 4800 MT/s |
| ECC | No |
| Maximum Supported | 128 GB |

---

# Motherboard

| Component | Value |
|----------|------|
| Manufacturer | Dell Inc. |
| Model | 0HR3HW |
| Revision | A00 |
| BIOS Vendor | Dell Inc. |
| BIOS Version | 1.6.1 |
| BIOS Release Date | 23 June 2025 |
| TPM | Enabled |
| UEFI | Enabled |

---

# Storage

## Boot Pool

| Device | Size | Purpose |
|---------|------|---------|
| SanDisk SD8SB8U-256G | 256 GB | TrueNAS boot-pool |

## Fast Pool

| Device | Size | Purpose |
|---------|------|---------|
| Samsung 990 PRO NVMe | 2 TB | Applications / High-speed storage |

## Main Storage Pool

| Item | Value |
|------|------|
| Pool | TerraMasterD4320 |
| Filesystem | ZFS |
| Layout | RAIDZ1 |
| Drives | 4 × 2 TB Western Digital |
| Usable Capacity | ~5.15 TiB |

## Physical Disk Inventory

The primary storage pool consists of four 2 TB Western Digital drives housed in a TerraMaster D4-320 enclosure.

| Bay | Linux Device | Model | Serial Number | RPM | Pool | Status |
|-----|--------------|-------|---------------|----:|------|--------|
| Bay 1 | /dev/sdb | WDC WD20EFRX-68EUZN0 | WD-WCC4M0EVVXSJ | 5400 | TerraMasterD4320 | Healthy |
| Bay 2 | /dev/sdc | WDC WD20EFRX-68EUZN0 | WD-WCC4M4HLR0NH | 5400 | TerraMasterD4320 | Healthy |
| Bay 3 | /dev/sdd | WDC WD2001FFSX-68JNUN0 | WD-WMC5C0E7W7FD | 7200 | TerraMasterD4320 | Healthy |
| Bay 4 | /dev/sde | WDC WD2001FFSX-68JNUN0 | WD-WMC160D2CAYF | 7200 | TerraMasterD4320 | Healthy |

### Notes

- Bays 1–2 are Western Digital Red NAS drives (5400 RPM).
- Bays 3–4 are Western Digital Red Pro NAS drives (7200 RPM).
- All drives support SMART monitoring.
- All drives are connected via SATA 6 Gb/s.
- The storage pool uses ZFS RAIDZ1.

## Storage Devices

| Device | Model | Capacity | Purpose |
|---------|-------|---------:|---------|
| /dev/sda | SanDisk SD8SB8U-256G-1006 | 256 GB | TrueNAS Boot Pool |
| /dev/nvme0n1 | Samsung SSD 990 PRO | 2 TB | Fast Pool |
| /dev/nvme1n1 | WD PC SN740 NVMe | 256 GB | Dell factory Windows SSD (currently unused by TrueNAS) |

## Storage Pools

| Pool | Device(s) | Purpose | Status |
|------|-----------|---------|--------|
| boot-pool | SanDisk 256 GB SSD | TrueNAS Operating System | Healthy |
| fast-pool | Samsung 990 PRO 2 TB | Applications / High-Speed Storage | Healthy |
| TerraMasterD4320 | 4 × WD Red Drives | Primary Media Storage | Healthy |

---

# Network

| Component | Value |
|----------|------|
| Primary Interface | enp128s31f6 |
| IP Address | 192.168.68.64 |
| Network | 192.168.68.0/22 |
| Gateway | 192.168.68.1 |
| Docker Networks | Multiple isolated bridge networks |

---

# Connected Storage

| Component | Value |
|----------|------|
| Enclosure | TerraMaster D4-320 |
| Bays | 4 |
| Connection | USB |

---

# Health Status

| Component | Status |
|----------|--------|
| Boot Pool | Healthy |
| Fast Pool | Healthy |
| TerraMasterD4320 | Healthy |
| Last Scrub | Completed successfully (0 errors) |

---

# Hardware Features

- Intel Quick Sync hardware transcoding
- Intel VT-x virtualization
- Intel VT-d IOMMU
- UEFI firmware
- ZFS RAIDZ1 storage
- Docker application hosting
- Virtual machine hosting
- SMB file sharing
- Snapshot protection