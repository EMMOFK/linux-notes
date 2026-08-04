# Backup Strategy

---

# Overview

This document defines the backup strategy for the home lab infrastructure.

The goal is to ensure that critical services can be restored quickly while avoiding unnecessary storage consumption.

The strategy combines:

- ZFS snapshots
- Configuration backups
- Virtual machine backups
- Documentation stored in GitHub
- Disaster recovery procedures

---

# Backup Objectives

Primary objectives:

- Protect important personal data.
- Recover from accidental deletion.
- Recover from hardware failure.
- Recover from software corruption.
- Minimise recovery time.
- Keep backup procedures simple and repeatable.

---

# Recovery Priorities

| Priority | Component |
|----------|-----------|
| 🔴 Critical | TrueNAS configuration |
| 🔴 Critical | Ubuntu BookStack VM |
| 🔴 Critical | BookStack documentation |
| 🔴 Critical | Immich photo library |
| 🟠 High | Docker configurations |
| 🟠 High | ARR configurations |
| 🟠 High | Application datasets |
| 🟡 Medium | Plex metadata |
| 🟢 Low | Movies and TV library |

---

# Current Backup Methods

| Component | Method |
|----------|--------|
| TrueNAS Configuration | Manual configuration export |
| Media Dataset | Weekly ZFS snapshots |
| Immich Dataset | Daily ZFS snapshots |
| Ubuntu VM | Manual VM backup |
| Documentation | GitHub Repository |

---

# ZFS Snapshot Strategy

## Media

| Setting | Value |
|----------|------|
| Frequency | Weekly |
| Retention | 4 Weeks |

Purpose:

Protects against accidental deletion while keeping storage usage under control.

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

Photographs change frequently and are significantly more valuable than replaceable media.

---

# TrueNAS Configuration Backup

Configuration exports should be created after:

- Storage changes
- Network changes
- User changes
- Installing new applications
- Major TrueNAS upgrades
- Snapshot policy changes

Recommended filename:

```
truenas-config-YYYY-MM-DD.db
```

Store configuration backups:

- On the Ubuntu VM
- In cloud storage
- On an external drive

---

# Ubuntu VM Backup

The Ubuntu Server VM should be backed up whenever significant changes are made.

Examples:

- New Docker containers
- Updated Docker Compose files
- Configuration changes
- Operating system upgrades

Critical data:

- Docker volumes
- BookStack
- Readarr
- Prowlarr
- SABnzbd
- Calibre-Web

---

# Documentation Backup

Infrastructure documentation is maintained in GitHub.

Repository contains:

- Infrastructure documentation
- Hardware inventory
- Network diagrams
- Storage architecture
- Disaster recovery procedures
- Linux notes

Benefits:

- Version history
- Off-site backup
- Easy recovery
- Documentation available from any device

---

# Data Classification

## Critical

Must be backed up.

Examples:

- TrueNAS configuration
- BookStack
- Immich
- Docker configurations

---

## Important

Should be backed up.

Examples:

- Plex metadata
- ARR configurations
- VM configuration

---

## Replaceable

Can be recreated.

Examples:

- Movies
- TV Shows
- Download cache
- Tdarr temporary files

---

# Restore Order

If complete recovery is required:

1. Restore TrueNAS.
2. Import ZFS pools.
3. Restore TrueNAS configuration.
4. Verify networking.
5. Restore Ubuntu VM.
6. Verify SMB shares.
7. Verify Docker services.
8. Verify snapshots.
9. Verify media applications.
10. Verify remote access.

---

# Backup Schedule

| Component | Frequency |
|-----------|-----------|
| Media Snapshot | Weekly |
| Immich Snapshot | Daily |
| TrueNAS Config Export | After major changes |
| Ubuntu VM Backup | After major changes |
| GitHub Documentation | After documentation updates |

---

# Future Improvements

Planned enhancements include:

- Automated TrueNAS configuration exports
- Scheduled Ubuntu VM backups
- Off-site backups
- 3-2-1 backup strategy
- Cloud backup for critical documentation
- UPS integration for clean shutdowns

---

# Design Philosophy

The backup strategy follows enterprise best practices:

- Prioritise irreplaceable data.
- Keep recovery procedures simple.
- Use layered backups.
- Document every recovery process.
- Store documentation off-site.
- Regularly test recovery procedures.