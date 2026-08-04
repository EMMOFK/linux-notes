# ARR Stack

---

# Overview

The ARR Stack is a collection of self-hosted applications that automate the discovery, acquisition, organisation and management of movies, TV shows and ebooks.

The system has been designed to minimise manual intervention by automatically searching for content, downloading it, organising it into the correct library and making it available to users.

The home lab currently operates two independent ARR environments:

- **Media Stack** (Movies & TV)
- **Book Stack** (eBooks)

---

# Purpose

The ARR Stack automates the complete media acquisition workflow.

Capabilities include:

- Automatic movie monitoring
- Automatic TV monitoring
- Automatic ebook monitoring
- Indexer management
- Usenet downloads
- Torrent downloads
- Automatic importing
- Library organisation
- Metadata management
- Configuration backup

The objective is to provide a fully automated media management platform requiring minimal manual intervention.

---

# Architecture

```text
                     USER
                      │
                      ▼
                 Overseerr
                      │
          ┌───────────┴───────────┐
          │                       │
          ▼                       ▼
       Radarr                  Sonarr
          │                       │
          └───────────┬───────────┘
                      ▼
                  Prowlarr
             ┌────────┴────────┐
             ▼                 ▼
         SABnzbd         qBittorrent
             │                 │
             └────────┬────────┘
                      ▼
             TerraMasterD4320
                      │
                      ▼
                   Tdarr
                      │
                      ▼
                    Plex
```

---

# Book Workflow

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

---

# Media Stack

Hosted on:

**TrueNAS SCALE**

| Application | Purpose |
|-------------|----------|
| Overseerr | Media requests |
| Radarr | Movie management |
| Sonarr | TV management |
| Prowlarr | Indexer management |
| SABnzbd | Usenet downloads |
| qBittorrent | Torrent downloads |
| Tdarr | Media optimisation |
| Clonarr | Configuration backup |

---

# Book Stack

Hosted on:

**Ubuntu Documentation & Library VM**

| Application | Purpose |
|-------------|----------|
| Readarr | Ebook management |
| Prowlarr | Book indexers |
| SABnzbd | Book downloads |
| Calibre-Web | Ebook library |

---

# Application Locations

## TrueNAS

| Service | URL |
|----------|-----|
| Overseerr | http://192.168.68.64:30002 |
| qBittorrent | http://192.168.68.64:30024 |
| Radarr | http://192.168.68.64:30025 |
| Prowlarr | http://192.168.68.64:30050 |
| SABnzbd | http://192.168.68.64:30055 |
| Sonarr | http://192.168.68.64:30113 |
| Tdarr | http://192.168.68.64:30088 |
| Clonarr | http://192.168.68.64:30427 |

---

## Ubuntu VM

| Service | URL |
|----------|-----|
| Readarr | http://192.168.68.59:8787 |
| Prowlarr | http://192.168.68.59:9696 |
| SABnzbd | http://192.168.68.59:8080 |
| Calibre-Web | http://192.168.68.59:8083 |

---

# Storage Layout

Media Library

```text
TerraMasterD4320
└── Media
    ├── Movies
    ├── TV Shows
    └── Tdarr_Transcode
```

Book Library

```text
TerraMasterD4320
└── Books
```

---

# Download Workflow

## Movies

1. User requests movie through Overseerr.
2. Radarr receives the request.
3. Radarr queries Prowlarr.
4. Prowlarr searches configured indexers.
5. Download is sent to SABnzbd or qBittorrent.
6. Download completes.
7. Radarr imports the movie.
8. Tdarr evaluates and optimises the file.
9. Plex updates the library.

---

## TV Shows

1. Sonarr monitors episodes.
2. Prowlarr searches indexers.
3. Download client retrieves content.
4. Sonarr imports the episode.
5. Tdarr evaluates the file.
6. Plex updates the TV library.

---

## Books

1. Readarr monitors wanted books.
2. Prowlarr searches book indexers.
3. SABnzbd downloads the ebook.
4. Readarr imports the book.
5. Book is organised into the Books library.
6. Calibre-Web serves the library.
7. Books are downloaded or read on the PocketBook e-reader.

---

# Indexers

Current strategy:

- NZBGeek (preferred)
- Public torrent indexers
- FlareSolverr where required

Preference order:

1. Usenet
2. Torrents

---

# Automation Features

Current automation includes:

- Automatic search
- Automatic downloads
- Automatic imports
- Automatic organisation
- Automatic metadata
- Automatic Plex updates
- Automatic Tdarr optimisation
- Automatic ARR configuration backups using Clonarr

---

# Backup Strategy

Critical data:

- ARR configuration
- Download client configuration
- Indexer configuration
- Clonarr backups

Media itself is considered replaceable.

Configuration is considered critical.

---

# Troubleshooting

Common issues encountered during deployment:

## Prowlarr

- Indexer priority configuration
- FlareSolverr integration
- Cloudflare protection

---

## Tdarr

- Intel Quick Sync configuration
- CPU fallback
- AV1 detection
- Subtitle preservation
- Health checks
- Snapshot cleanup after optimisation

---

## Downloads

- Category mapping
- Root folders
- Import paths
- Permissions
- Hardlink configuration

---

# Lessons Learned

Building the ARR ecosystem highlighted several important engineering principles:

- Separate media services from documentation services.
- Prefer Usenet over torrents when possible for reliability and speed.
- Keep application configurations backed up using Clonarr.
- Store media on resilient ZFS datasets.
- Optimise media after import rather than during download.
- Test automation workflows end-to-end after making configuration changes.
- Use infrastructure documentation to record configuration decisions and recovery procedures.

---

# Future Improvements

Planned enhancements:

- Reverse proxy with HTTPS
- Internal DNS names
- Grafana dashboards
- Additional indexers
- Off-site configuration backups
- Automated health monitoring
- Automated update notifications

---

# Design Philosophy

The ARR Stack is designed to minimise manual administration while maintaining full control over media acquisition and organisation.

By separating the media stack from the documentation and ebook platform, the home lab remains modular, easier to maintain and simpler to recover.

Configuration and automation are considered more valuable than the media itself, as the library can be recreated but the automation workflows represent significant engineering effort.