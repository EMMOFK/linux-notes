# Plex Media Server

---

# Overview

Plex Media Server is the primary media streaming platform within the home lab.

It provides a central interface for streaming movies and television shows to supported devices while integrating with the automated ARR media management stack.

Media is automatically acquired, organised, optimised and made available through Plex with minimal manual intervention.

---

# Purpose

Plex serves as the front-end of the media platform.

Its responsibilities include:

- Streaming Movies
- Streaming TV Shows
- Library management
- Metadata retrieval
- Artwork downloads
- Watch history
- User management
- Hardware accelerated transcoding
- Remote streaming (future)

Plex is considered the primary consumer-facing application within the media stack.

---

# System Information

| Item | Value |
|------|-------|
| Host | TrueNAS SCALE |
| IP Address | 192.168.68.64 |
| URL | http://192.168.68.64:32400 |
| Platform | TrueNAS Applications |
| Status | Production |

---

# Storage

Plex itself runs on the **fast-pool** through the TrueNAS Applications system.

The media library is stored separately on the **TerraMasterD4320** ZFS pool.

This separation ensures that application performance is not affected by large media files while allowing the media library to scale independently.

Media location:

```text
TerraMasterD4320
└── Media
    ├── Movies
    └── TV Shows
```

---

# Library Structure

Current libraries include:

| Library | Location |
|----------|----------|
| Movies | TerraMasterD4320/Media/Movies |
| TV Shows | TerraMasterD4320/Media/TV Shows |

Future libraries may include:

- Music
- Home Videos
- Audiobooks

---

# Hardware Transcoding

Plex uses Intel Quick Sync Video (QSV) for hardware-accelerated transcoding.

Benefits include:

- Lower CPU utilisation
- Faster transcodes
- Reduced power consumption
- Support for multiple simultaneous streams

This allows the server to stream media efficiently without placing unnecessary load on the CPU.

---

# Integration

Plex is tightly integrated with the rest of the media ecosystem.

```text
User
   │
   ▼
Overseerr
   │
   ▼
Radarr / Sonarr
   │
   ▼
Prowlarr
   │
   ▼
SABnzbd / qBittorrent
   │
   ▼
Media Library
   │
   ▼
Tdarr
   │
   ▼
Plex
```

Workflow:

1. User requests media through Overseerr.
2. Radarr or Sonarr manages the request.
3. Prowlarr searches configured indexers.
4. SABnzbd or qBittorrent downloads the content.
5. Media is imported into the library.
6. Tdarr optimises the file where required.
7. Plex detects the new media and updates the library.

---

# Dependencies

Plex depends on:

- TrueNAS SCALE
- fast-pool application storage
- TerraMasterD4320 media dataset
- Radarr
- Sonarr
- Tdarr
- SMB storage
- Intel Quick Sync

---

# Backup Strategy

Critical components:

- Plex configuration
- Plex metadata
- Library settings

Media files themselves are protected through ZFS snapshots.

Because movies and TV shows are considered replaceable, configuration and metadata are prioritised over the media itself.

---

# Recovery Procedure

Recovery steps:

1. Restore TrueNAS.
2. Restore applications.
3. Restore Plex configuration.
4. Verify media datasets are mounted.
5. Scan libraries.
6. Verify hardware transcoding.
7. Test playback.

---

# Performance Optimisation

Current optimisations include:

- Application stored on SSD
- Media stored on RAIDZ1
- Intel Quick Sync enabled
- Tdarr optimisation pipeline
- HEVC preferred where appropriate
- Automatic metadata downloads

---

# Current Environment

Media acquisition is almost fully automated.

Automation includes:

- Movie requests
- TV requests
- Automatic downloads
- Automatic organisation
- Metadata retrieval
- Library updates
- Media optimisation

Minimal manual intervention is required after the initial request.

---

# Security

Current deployment:

- Accessible only on the local network
- Remote access available through Tailscale
- No direct public exposure
- User authentication enabled

Future improvements:

- HTTPS reverse proxy
- Internal DNS
- Secure remote streaming
- Multi-user profiles

---

# Maintenance

Routine maintenance includes:

- Updating the Plex application
- Monitoring storage utilisation
- Checking hardware transcoding
- Reviewing library integrity
- Verifying automatic scans
- Monitoring application logs

---

# Troubleshooting

## Library not updating

- Verify Radarr/Sonarr import completed.
- Check library paths.
- Run a manual scan.

---

## Playback buffering

- Verify Intel Quick Sync is active.
- Check CPU utilisation.
- Confirm media is stored on the correct dataset.

---

## Metadata missing

- Refresh metadata.
- Verify internet connectivity.
- Check Plex metadata agents.

---

## Hardware transcoding unavailable

- Confirm Intel GPU is passed through correctly.
- Verify Plex has access to Quick Sync.
- Check application logs.

---

# Lessons Learned

Building the Plex environment reinforced several key infrastructure principles:

- Separate applications from media storage.
- Automate media acquisition wherever possible.
- Optimise media after download rather than during download.
- Hardware transcoding significantly improves performance.
- ZFS snapshots protect libraries from accidental deletion.
- Document configuration decisions as the environment evolves.

---

# Future Improvements

Planned enhancements include:

- HTTPS with reverse proxy
- Internal DNS records
- Automated configuration backups
- Monitoring through Prometheus
- Grafana dashboards
- Additional media libraries
- Secure external streaming

---

# Design Philosophy

Plex is the presentation layer of the home media platform.

The surrounding infrastructure—including the ARR Stack, Tdarr, ZFS storage and TrueNAS—is designed to support Plex by providing an automated, reliable and scalable media ecosystem.

The overall objective is to minimise manual administration while delivering a fast, resilient and self-hosted streaming experience.