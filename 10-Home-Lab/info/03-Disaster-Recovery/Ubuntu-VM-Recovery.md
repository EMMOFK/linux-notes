# Ubuntu BookStack VM Recovery

---

# Overview

This document describes the recovery procedure for the Ubuntu BookStack virtual machine.

The objective is to restore the VM to full operational status following:

- Virtual machine corruption
- Accidental deletion
- Failed operating system upgrade
- Storage migration
- Hardware failure
- Complete TrueNAS rebuild

This document assumes that the TrueNAS server has already been restored successfully.

---

# Recovery Objectives

Restore the following services:

- Ubuntu Server
- Docker Engine
- Docker Compose
- BookStack
- Readarr
- Prowlarr
- SABnzbd
- Calibre-Web

The VM should be restored with its original IP address and reconnect to all required storage.

---

# VM Information

| Item | Value |
|------|-------|
| Host | TrueNAS |
| Operating System | Ubuntu Server |
| Purpose | Docker Host |
| Storage Pool | fast-pool |
| IP Address | 192.168.68.59 |

---

# Recovery Requirements

Before beginning recovery ensure the following are available:

- TrueNAS fully operational
- fast-pool imported
- Latest Ubuntu Server ISO
- Docker installation instructions
- Latest Docker Compose files
- Latest Docker volume backup
- GitHub Infrastructure Documentation

---

# Recovery Procedure

## Step 1 — Restore the Virtual Machine

If a VM backup exists:

Restore the backup into TrueNAS.

Otherwise:

Create a new Ubuntu Server virtual machine.

Recommended specifications:

| Component | Value |
|-----------|-------|
| Operating System | Ubuntu Server LTS |
| Storage | fast-pool |
| CPU | Match previous configuration |
| RAM | Match previous configuration |
| Network | Bridged |

---

## Step 2 — Configure Networking

Assign the original static IP.

| Setting | Value |
|----------|------|
| IP Address | 192.168.68.59 |
| Gateway | 192.168.68.1 |
| DNS | Current LAN DNS |

Verify:

- Internet connectivity
- Access to TrueNAS
- DNS resolution

---

## Step 3 — Update Ubuntu

Run system updates.

Example:

```bash
sudo apt update
sudo apt upgrade
```

Reboot if required.

---

## Step 4 — Install Docker

Install:

- Docker Engine
- Docker Compose

Verify installation:

```bash
docker --version
docker compose version
```

---

## Step 5 — Restore Docker Configuration

Restore:

- Docker Compose files
- Environment files (.env)
- Configuration directories
- Persistent Docker volumes

Verify all expected directories are present before continuing.

---

## Step 6 — Restore Containers

Start the Docker stack.

Verify that the following containers start successfully:

- BookStack
- Readarr
- Prowlarr
- SABnzbd
- Calibre-Web

Confirm all containers report a healthy status.

---

## Step 7 — Verify Storage Access

Confirm the VM can access any required SMB shares hosted on TrueNAS.

Expected storage includes:

- Books
- Media (if required)
- Shared datasets

Verify read and write permissions.

---

## Step 8 — Verify Services

Open each web interface.

| Service | URL |
|----------|-----|
| BookStack | http://192.168.68.59:6875 |
| Readarr | http://192.168.68.59:8787 |
| Prowlarr | http://192.168.68.59:9696 |
| SABnzbd | http://192.168.68.59:8080 |
| Calibre-Web | http://192.168.68.59:8083 |

Verify each application loads correctly.

---

## Step 9 — Verify Connectivity

Confirm the VM can communicate with:

- TrueNAS
- Internet
- Docker network
- SMB shares

Verify:

- Readarr can reach Prowlarr
- Readarr can reach SABnzbd
- BookStack is accessible
- Calibre-Web detects the library

---

## Step 10 — Final Validation

Confirm:

- Ubuntu fully updated
- Docker healthy
- All containers running
- Correct static IP
- BookStack functioning
- Readarr operational
- Prowlarr operational
- SABnzbd operational
- Calibre-Web operational

---

# Recovery Checklist

- Ubuntu restored
- Docker installed
- Docker Compose restored
- Volumes restored
- Containers started
- Network verified
- SMB shares mounted
- Services tested
- Documentation updated (if recovery required changes)

---

# Estimated Recovery Time

| Task | Estimated Time |
|------|----------------|
| Install Ubuntu | 15–20 minutes |
| Install Docker | 10 minutes |
| Restore Configuration | 15 minutes |
| Restore Containers | 10 minutes |
| Testing | 10 minutes |

Estimated total:

**Approximately 1 hour**

---

# Future Improvements

Planned enhancements include:

- Docker Compose stored in GitHub
- Automated nightly VM backups
- Automated Docker volume backups
- Restore script for Docker services
- Configuration management using Infrastructure as Code

---

# Recovery Philosophy

The Ubuntu BookStack VM is intentionally independent from the media stack.

Its recovery process is designed to be:

- Simple
- Repeatable
- Well documented
- Independent of the TrueNAS operating system

Infrastructure documentation stored in GitHub provides an off-site reference for rebuilding the environment if local documentation is unavailable.