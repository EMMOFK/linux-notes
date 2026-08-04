# Home Lab Networking

---

# Overview

This section documents the network infrastructure of the home lab.

It provides a complete overview of how devices communicate, how services are accessed, and how remote connectivity is securely managed.

The goal is to maintain clear documentation that simplifies troubleshooting, disaster recovery, future upgrades, and ongoing administration.

The network has been designed with the following priorities:

- Reliability
- Security
- Simplicity
- Scalability
- Remote management

---

# Network Objectives

The home lab network has been designed to:

- Provide reliable access to all self-hosted services.
- Separate infrastructure from user devices through static addressing.
- Support secure remote administration.
- Minimise downtime during maintenance.
- Provide a platform for learning enterprise networking concepts.
- Support future expansion without major redesign.

---

# Current Network

Current LAN:

```
192.168.68.0/22
```

Gateway:

```
192.168.68.1
```

Current DNS:

```
TP-Link Deco Router
```

Remote access:

```
Tailscale VPN
```

---

# Core Infrastructure

The network currently consists of the following primary systems.

| Device | Role |
|---------|------|
| TP-Link Deco | Internet gateway and DHCP server |
| TrueNAS SCALE | Primary storage server |
| Ubuntu Server VM | Docker host for documentation and ebook services |
| Linux Laptop | Administration workstation |
| Desktop PC | Primary management workstation |

---

# Documentation Structure

This section is organised into several documents covering different areas of the network.

## IP Addressing

Documents:

- LAN addressing
- Static IP allocations
- DHCP strategy
- Reserved address ranges

---

## DNS

Documents:

- Current DNS configuration
- Planned AdGuard Home deployment
- Future DNS improvements

---

## Tailscale

Documents:

- Remote access architecture
- Secure administration
- VPN topology
- Device connectivity

---

## SMB and File Shares

Documents:

- Shared folders
- SMB permissions
- Linux mounts
- Windows access
- TrueNAS datasets

---

## Firewall and Security

Documents:

- Remote access policy
- Network security
- Service exposure
- Administrative access

---

## Future Network

Documents:

- Planned upgrades
- VLAN implementation
- Faster networking
- Enterprise features

---

# Design Principles

The network follows several core principles.

## Security First

Services are kept private whenever possible.

Remote administration is performed through Tailscale rather than exposing services directly to the Internet.

---

## Static Infrastructure

Servers use static IP addresses.

This simplifies:

- Documentation
- DNS
- Troubleshooting
- Disaster recovery

---

## Separation of Responsibilities

Each system has a dedicated role.

| System | Responsibility |
|----------|----------------|
| TrueNAS | Storage, media services, photo management |
| Ubuntu VM | Documentation, ebooks and supporting Docker services |
| Linux Laptop | Administration |
| TP-Link Deco | Routing, DHCP and Internet connectivity |

---

## Documentation Driven

Every significant component of the network is documented.

This repository serves as the authoritative source for:

- Network topology
- Service locations
- Infrastructure design
- Recovery procedures
- Future expansion plans

---

# Future Goals

Planned improvements include:

- AdGuard Home as the primary DNS server
- UPS monitoring and automatic shutdown
- 2.5 GbE networking
- VLAN segmentation
- Reverse proxy with HTTPS
- Monitoring and alerting
- Enterprise-style network documentation
- Automated infrastructure backups

---

# Summary

The networking documentation provides a complete reference for the home lab environment.

By maintaining accurate documentation alongside the infrastructure itself, the network becomes easier to manage, troubleshoot, recover, and expand while also serving as a practical learning resource for networking, Linux, virtualization, and enterprise infrastructure.