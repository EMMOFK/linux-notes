# Home Lab

---

# Overview

This repository documents my production home lab environment.

The primary goals of this lab are to:

- Learn enterprise networking
- Learn Linux administration
- Learn Docker and containers
- Learn virtualization
- Learn storage technologies
- Learn backup and disaster recovery
- Build production-quality infrastructure documentation
- Prepare for a career in Network Engineering

Although this began as a learning environment, it now hosts production services that store important personal data alongside replaceable media.

---

# Environment Status

**Production**

Core services are running continuously and are protected using ZFS snapshots, documented recovery procedures and configuration backups.

---

# Infrastructure Documentation

## Infrastructure

- Hardware Inventory
- TrueNAS Infrastructure
- Ubuntu BookStack VM
- Storage Architecture
- Network Diagram
- Services and Ports

---

## Applications

- Tailscale

- Bookstack vm server
 
- readarr 
 
- Bookstack vm prowlarr
 
- Bookstack Vm SabNZB
 
- Calibre web
 
- Plex
 
- immich

- homarr

- tdarr

- clonarr

- overseer

- qbittorent

- sonnarr

- radarr

- Movie stack prowlarr

- Movie Stack SABnzb


---

## Disaster Recovery

- TrueNAS Recovery
- Ubuntu VM Recovery
- Backup Strategy

---

## Networking

- IP Addressing
- DNS
- VLANs
- Remote Access

---

# Core Infrastructure

## Storage

- TrueNAS SCALE
- ZFS
- RAIDZ1
- Weekly snapshots
- Daily snapshots for critical data

## Virtualization

- Ubuntu Server virtual machine
- Docker workloads
- BookStack documentation server

## Media Stack

- Plex
- Radarr
- Sonarr
- Prowlarr
- SABnzbd
- qBittorrent
- Tdarr
- Overseerr

## Self Hosted Services

- Immich
- BookStack
- Homarr
- AdGuard Home
- Prometheus
- Clonarr
- FlareSolverr

---

# Current Infrastructure

## TrueNAS Server

Dell Pro Max Slim FCS1250

Primary storage server

IP:

192.168.68.64

---

## Ubuntu Docker VM

BookStack

Readarr

Calibre-Web

Docker host

IP:

192.168.68.59

---

# Design Philosophy

This home lab follows enterprise infrastructure principles:

- Separate operating system from data.
- Separate SSD and HDD workloads.
- Document everything.
- Automate wherever practical.
- Design for recovery before failure.
- Build with scalability in mind.

---

# Documentation Standards

Each document in this repository aims to answer:

- What does this service do?
- Why does it exist?
- Where is it stored?
- How is it backed up?
- How is it restored?
- What depends on it?

---

# Current Status

✔ Production Environment

✔ Infrastructure documented

✔ Storage architecture documented

✔ Disaster recovery documentation in progress

✔ Continuing to expand application and networking documentation