# Tailscale

---

# Overview

Tailscale provides secure remote access to the home lab using a private WireGuard-based mesh VPN.

Rather than exposing services directly to the Internet through port forwarding, Tailscale creates an encrypted private network that allows trusted devices to communicate securely from anywhere.

Tailscale is the primary remote administration solution for the home lab.

---

# Purpose

Tailscale provides:

- Secure remote access
- Encrypted communications
- Private networking
- Access without port forwarding
- Secure administration
- Remote troubleshooting

---

# System Information

| Item | Value |
|------|-------|
| Platform | TrueNAS SCALE |
| Technology | WireGuard Mesh VPN |
| Status | Production |

---

# Protected Services

Current remote access includes:

- TrueNAS Web Interface
- Plex
- Immich
- Homarr
- Tdarr
- ARR Stack
- Ubuntu Documentation & Library VM
- BookStack
- Calibre-Web

---

# Architecture

```text
Remote Device
      │
      ▼
Encrypted Tailscale Tunnel
      │
      ▼
TrueNAS Server
      │
      ├── Applications
      │
      └── Ubuntu VM
```

---

# Advantages

Current benefits include:

- No port forwarding
- End-to-end encryption
- Private network
- Device authentication
- Simple deployment
- Secure administration

---

# Security

Current security model:

- Zero Trust networking
- WireGuard encryption
- Device authentication
- No public services exposed

---

# Backup Strategy

Critical components:

- Tailscale account
- Device authorisation
- Network configuration

Configuration is included within the TrueNAS recovery documentation.

---

# Recovery Procedure

Recovery steps:

1. Restore TrueNAS.
2. Install Tailscale.
3. Authenticate the server.
4. Verify remote connectivity.
5. Test application access.

---

# Maintenance

Routine maintenance includes:

- Updating Tailscale
- Removing unused devices
- Reviewing access permissions
- Verifying connectivity

---

# Troubleshooting

## Cannot connect

- Verify Internet connectivity.
- Confirm Tailscale service is running.
- Verify device authentication.

---

## Services unreachable

- Verify the target application is running.
- Confirm firewall configuration.
- Verify the destination IP address.

---

# Lessons Learned

Using Tailscale demonstrated several important networking principles:

- VPN access is significantly more secure than exposing management ports.
- WireGuard provides excellent performance with minimal configuration.
- Remote administration becomes much simpler when all devices participate in the same private network.

---

# Future Improvements

Planned enhancements:

- Additional trusted devices
- Exit node evaluation
- Subnet router evaluation
- Monitoring integration

---

# Design Philosophy

Remote administration should always prioritise security over convenience.

Tailscale provides encrypted access to the home lab while eliminating the need for public port forwarding, reducing the attack surface of the entire environment.