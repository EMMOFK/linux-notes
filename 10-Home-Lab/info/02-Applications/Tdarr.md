# Tdarr

---

# Overview

Tdarr is the automated media optimisation platform within the home lab.

Its primary purpose is to analyse the media library and optimise video files by converting inefficient codecs into more storage-efficient formats while preserving playback compatibility and media quality.

Tdarr operates automatically after Radarr and Sonarr import media into the library, ensuring that newly acquired content is optimised before long-term storage.

---

# Purpose

Tdarr was deployed to achieve several objectives:

- Reduce storage consumption
- Standardise media codecs
- Preserve media quality
- Reduce bandwidth requirements
- Improve Plex Direct Play compatibility
- Automate media optimisation
- Minimise manual transcoding

Rather than manually re-encoding media, Tdarr continuously processes the library in the background.

---

# System Information

| Item | Value |
|------|-------|
| Host | TrueNAS SCALE |
| Platform | TrueNAS Applications |
| URL | http://192.168.68.64:30088 |
| Status | Production |
| Hardware Acceleration | Intel Quick Sync Video |

---

# Storage

The Tdarr application runs on the TrueNAS application storage while processing media stored on the TerraMasterD4320 ZFS pool.

Media Library

```
TerraMasterD4320
└── Media
    ├── Movies
    ├── TV Shows
    └── Tdarr_Transcode
```

Temporary transcoding files are written to the **Tdarr_Transcode** directory before replacing the original media.

---

# Architecture

```
Radarr / Sonarr
        │
        ▼
Media Library
        │
        ▼
      Tdarr
        │
        ▼
Codec Analysis
        │
        ▼
Intel Quick Sync
        │
        ▼
HEVC Output
        │
        ▼
Replace Original File
        │
        ▼
Plex Library
```

---

# Optimisation Strategy

The current optimisation policy is designed to maximise storage efficiency while avoiding unnecessary transcoding.

Current behaviour:

- Skip HEVC media
- Skip AV1 media
- Convert H.264 media to HEVC
- Convert MPEG-2 media to HEVC
- Convert VC-1 media to HEVC
- Skip unsupported legacy formats where appropriate
- Preserve subtitles
- Preserve preferred audio tracks

This ensures only media that benefits from transcoding is processed.

---

# Processing Workflow

Current processing sequence:

1. Scan media library.
2. Analyse video codec.
3. Skip HEVC media.
4. Skip AV1 media.
5. Transcode supported codecs.
6. Preserve subtitles.
7. Preserve audio.
8. Verify output file.
9. Replace original media.
10. Update Plex library.

---

# Hardware Acceleration

Tdarr uses Intel Quick Sync Video (QSV) to accelerate transcoding.

Benefits include:

- Faster transcoding
- Lower CPU utilisation
- Lower power consumption
- Ability to process multiple files simultaneously

Hardware transcoding significantly reduced overall processing time compared with CPU-only encoding.

---

# Results

Following the initial optimisation run:

| Metric | Result |
|---------|---------|
| Successful Transcodes | 829 |
| Failed Files | Legacy formats only |
| Space Recovered | Approximately 1.25 TiB |
| Media Library | Successfully optimised |

The optimisation project substantially increased available storage while maintaining library quality.

---

# Snapshot Management

Prior to optimisation, a ZFS snapshot of the media dataset was created.

After successful verification:

- Obsolete snapshots removed
- 74 historical snapshots deleted
- Approximately 2 TiB of snapshot references released
- New baseline snapshot created

Current baseline:

```
post-tdarr-optimized-2026-08-04
```

This ensures future recovery begins from an already optimised media library.

---

# Integration

Tdarr integrates with the wider media ecosystem.

```
Overseerr
      │
      ▼
Radarr / Sonarr
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

Tdarr operates automatically after media has been imported by Radarr or Sonarr.

---

# Backup Strategy

Critical components:

- Tdarr Flow configuration
- Node configuration
- Library configuration
- Plugin settings

Media itself is protected through ZFS snapshots.

Because the optimisation workflow required significant engineering effort, the Tdarr configuration is considered more valuable than individual media files.

---

# Recovery Procedure

Recovery steps:

1. Restore TrueNAS.
2. Restore Tdarr application.
3. Restore Tdarr configuration.
4. Verify media paths.
5. Verify Intel Quick Sync.
6. Verify worker nodes.
7. Perform test transcode.
8. Resume automatic processing.

---

# Performance Optimisation

Current optimisations include:

- Intel Quick Sync enabled
- SSD application storage
- Dedicated transcode directory
- Automatic file replacement
- Subtitle preservation
- Audio preservation
- Codec-aware processing
- AV1 skipping
- HEVC skipping

---

# Troubleshooting

## Intel Quick Sync unavailable

- Verify GPU assignment.
- Confirm hardware transcoding is enabled.
- Review Tdarr logs.

---

## Files repeatedly processed

- Verify codec detection.
- Confirm HEVC and AV1 skip rules.
- Review Flow configuration.

---

## Health check failures

Typical causes include:

- Legacy AVI containers
- Rawvideo files
- Unsupported codecs

These files may require manual review or exclusion from automated processing.

---

## Failed transcodes

Check:

- Available storage
- File permissions
- Hardware acceleration
- FFmpeg logs

---

# Lessons Learned

Deploying Tdarr provided several valuable lessons:

- Always create a ZFS snapshot before bulk media operations.
- Snapshot space can hide reclaimed storage until obsolete snapshots are removed.
- Hardware transcoding dramatically improves processing performance.
- Optimising only inefficient codecs prevents unnecessary work.
- Preserve subtitles and preferred audio tracks whenever possible.
- Verify optimisation workflows with a small test library before processing the full collection.
- Document Flow changes to make future troubleshooting easier.

---

# Future Improvements

Planned enhancements include:

- Automatic CPU fallback if Intel Quick Sync fails
- Automatic exclusion of unsupported legacy formats
- Improved handling of VC-1 content
- Additional health check automation
- Tdarr monitoring through Prometheus
- Grafana dashboards
- Scheduled optimisation reports

---

# Design Philosophy

Tdarr is responsible for ensuring the media library remains storage-efficient without compromising playback quality.

The optimisation workflow is designed to process only media that benefits from transcoding while avoiding unnecessary re-encoding of modern codecs.

By combining Intel Quick Sync, ZFS snapshots, and automated processing, Tdarr provides an efficient, reliable and largely hands-off media optimisation platform that integrates seamlessly with the wider home lab ecosystem.