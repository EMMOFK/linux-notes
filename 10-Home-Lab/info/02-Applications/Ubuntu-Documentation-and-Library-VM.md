# Ubuntu Documentation & Library VM

---

# Overview

This virtual machine provides a dedicated Ubuntu Server environment for hosting self-contained Docker services that support both technical documentation and digital library management.

Separating these workloads from the TrueNAS host provides several advantages:

- Independent operating system
- Simplified Docker management
- Isolation from storage services
- Easier maintenance and upgrades
- Improved disaster recovery
- Hands-on Linux administration experience

The VM serves as a dedicated Docker host for two primary workloads:

- **Technical Documentation** using BookStack
- **Digital Library Management** using Readarr, Prowlarr, SABnzbd and Calibre-Web

Together these services provide a complete self-hosted platform for managing technical knowledge and a personal ebook library.

---

# System Information

| Item | Value |
|------|-------|
| Operating System | Ubuntu Server |
| Virtualization Platform | TrueNAS SCALE |
| Host Server | TrueNAS |
| Purpose | Docker Services Host |
| Status | Production |
| IP Address | 192.168.68.59 |
| Storage Pool | fast-pool |

---

# Purpose

The Ubuntu Server VM performs two critical roles within the home lab.

## Technical Documentation

The VM hosts BookStack, which serves as the central knowledge base for the entire home lab.

Documentation includes:

- Linux administration
- TrueNAS documentation
- Networking
- CCNA study notes
- Disaster recovery procedures
- Home lab documentation
- Infrastructure documentation
- Personal technical notes

BookStack is considered a critical service because it stores the operational knowledge required to maintain and recover the home lab.

---

## Digital Library

The VM also hosts a complete self-hosted ebook management platform.

The digital library provides:

- Automatic book discovery
- Ebook downloads through Usenet
- Metadata management
- EPUB library organisation
- Web-based ebook library
- Reading on a PocketBook e-reader

This provides a fully self-hosted alternative to commercial ebook ecosystems while maintaining complete ownership of the library.

---

# Storage

The virtual machine is stored on the **fast-pool** NVMe SSD within TrueNAS.

Benefits include:

- Faster VM boot times
- Improved Docker performance
- Low latency
- High IOPS
- Faster database access
- Better application responsiveness

Underlying storage:

| Component | Value |
|----------|------|
| Storage Pool | fast-pool |
| Device | Samsung 990 PRO 2 TB NVMe |

---

# Hosted Services

| Service | URL | Purpose |
|----------|-----|----------|
| BookStack | http://192.168.68.59:6875 | Technical documentation and knowledge base |
| Readarr | http://192.168.68.59:8787 | Ebook management |
| Prowlarr | http://192.168.68.59:9696 | Book indexer management |
| SABnzbd | http://192.168.68.59:8080 | Usenet downloader |
| Calibre-Web | http://192.168.68.59:8083 | Web-based ebook library |

---

# Docker Environment

The Ubuntu VM functions as a dedicated Docker host.

Current containers include:

- BookStack
- Readarr
- Prowlarr
- SABnzbd
- Calibre-Web

These containers provide two distinct service groups.

## Documentation Platform

BookStack stores documentation covering:

- Home Lab
- Linux
- TrueNAS
- Networking
- Docker
- Virtualization
- Disaster Recovery
- CCNA
- Infrastructure

Documentation is also maintained within the GitHub repository, providing version control and an off-site backup.

---

## Digital Library Platform

Readarr, Prowlarr, SABnzbd and Calibre-Web work together to create an automated ebook management workflow.

Workflow:

```text
Readarr
    │
    ▼
Prowlarr
    │
    ▼
SABnzbd
    │
    ▼
Books Library
    │
    ▼
Calibre-Web
    │
    ▼
PocketBook e-reader
```

The system automatically discovers, downloads, organises and serves EPUB books for reading on a PocketBook e-reader.

---

# Network Configuration

| Setting | Value |
|----------|------|
| Hostname | Ubuntu Server VM |
| IP Address | 192.168.68.59 |
| Protocol | HTTP |
| Docker Host | Yes |

The VM communicates with:

- TrueNAS SCALE
- SMB shares
- Internet
- Docker bridge network

---

# Integration with TrueNAS

The Ubuntu VM complements the TrueNAS host by separating documentation and digital library services from media services.

## TrueNAS Responsibilities

- ZFS storage
- Snapshots
- SMB shares
- Media services
- Virtualization
- Infrastructure applications

## Ubuntu VM Responsibilities

- Documentation
- Docker services
- Ebook management
- Linux workloads
- Digital library platform

This separation improves maintainability, performance and disaster recovery.

---

# Backup Strategy

Critical data includes:

- Docker Compose files
- Docker volumes
- BookStack database
- BookStack uploads
- Readarr configuration
- Prowlarr configuration
- SABnzbd configuration
- Calibre-Web configuration

Recovery is performed as part of the Ubuntu VM disaster recovery procedure.

---

# Recovery Procedure

Recovery consists of:

1. Restore the Ubuntu virtual machine.
2. Install Docker Engine.
3. Restore Docker Compose files.
4. Restore Docker volumes.
5. Restore application configuration.
6. Verify network connectivity.
7. Verify access to TrueNAS storage.
8. Test all hosted services.

---

# Current Usage

The VM currently supports two production workloads.

## Technical Documentation

BookStack acts as the operational knowledge base for the home lab and contains documentation covering:

- Linux
- Networking
- Docker
- TrueNAS
- Disaster Recovery
- Home Lab
- CCNA
- Infrastructure

---

## Digital Library

The VM provides a complete self-hosted ebook ecosystem.

Current capabilities include:

- Automatic book discovery
- Usenet downloads
- Metadata management
- EPUB library organisation
- Web-based ebook access
- Reading on a PocketBook e-reader

The complete workflow is automated from discovering a book through to reading it on the PocketBook device.

---

# Security

Current deployment:

- Hosted on the trusted LAN
- Remote access available through Tailscale
- Not publicly exposed to the Internet
- Protected by Ubuntu user authentication

Future improvements:

- HTTPS
- Reverse proxy
- Automatic certificate renewal
- Single Sign-On (SSO)

---

# Maintenance

Routine maintenance includes:

- Updating Ubuntu
- Updating Docker images
- Monitoring container health
- Verifying backups
- Reviewing storage usage
- Updating documentation

---

# Troubleshooting

## BookStack unavailable

- Verify the Ubuntu VM is running.
- Verify Docker is running.
- Confirm the BookStack container is healthy.
- Check Docker logs.
- Verify port 6875 is listening.

## Readarr or Calibre-Web unavailable

- Verify Docker containers are running.
- Confirm network connectivity.
- Check Docker logs.
- Verify storage access.

## Performance issues

- Verify VM resources.
- Check Docker resource usage.
- Monitor SSD utilisation.
- Confirm fast-pool health.

---

# Future Improvements

Planned enhancements include:

- HTTPS
- Reverse proxy
- Automated Docker updates
- Automated database backups
- Infrastructure monitoring
- Health checks
- Automated restore testing

---

# Design Philosophy

The Ubuntu VM is a dedicated Docker services platform built around two core objectives:

1. Centralising technical knowledge through BookStack.
2. Providing a fully self-hosted digital library for managing and reading EPUB books on a PocketBook e-reader.

By separating these services from the TrueNAS host, the home lab remains modular, easier to maintain and simpler to recover following a failure.

The VM is considered a critical component of the home lab infrastructure and forms an essential part of the overall disaster recovery strategy.