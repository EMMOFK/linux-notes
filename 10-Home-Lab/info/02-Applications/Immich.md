# Immich

---

# Overview

Immich is the self-hosted photo and video management platform within the home lab.

It provides secure storage, automatic organisation and mobile synchronisation for personal photographs and videos while keeping all data under local control.

Unlike the media library, which stores replaceable content, the Immich library contains irreplaceable personal memories and is therefore considered one of the most critical services within the home lab.

---

# Purpose

Immich provides a private alternative to cloud photo services.

Primary features include:

- Automatic photo backup
- Automatic video backup
- Mobile synchronisation
- Timeline view
- Face recognition
- Location mapping
- Albums
- Metadata management
- Web interface
- Multi-device access

---

# System Information

| Item | Value |
|------|-------|
| Host | TrueNAS SCALE |
| Platform | TrueNAS Applications |
| URL | http://192.168.68.64:30041 |
| Status | Production |

---

# Storage

Immich stores its photo library on the TerraMasterD4320 storage pool.

Dataset:

```text
TerraMasterD4320
└── Immich
```

Application data is stored separately from the media library to simplify backups and recovery.

---

# Architecture

```text
Mobile Devices
        │
        ▼
      Immich
        │
        ▼
 Photo Library
        │
        ▼
TerraMasterD4320
```

---

# Features

Current capabilities include:

- Automatic uploads
- Automatic organisation
- Timeline browsing
- Web gallery
- Metadata storage
- Search
- Album management
- Mobile application support

---

# Backup Strategy

Immich is considered critical.

Current protection:

- Daily ZFS snapshots
- Two-week retention
- Included in disaster recovery documentation

Unlike the media library, photographs are considered irreplaceable.

---

# Recovery Procedure

Recovery consists of:

1. Restore TrueNAS.
2. Restore Immich application.
3. Import the Immich dataset.
4. Verify database.
5. Verify photo library.
6. Test mobile synchronisation.

---

# Security

Current deployment:

- Local network access
- Remote access through Tailscale
- No public Internet exposure

Future improvements:

- HTTPS
- Reverse proxy
- Off-site photo backup

---

# Maintenance

Routine maintenance includes:

- Updating Immich
- Verifying mobile uploads
- Monitoring storage usage
- Reviewing snapshot status
- Checking application health

---

# Troubleshooting

## Upload failures

- Verify storage capacity.
- Confirm dataset permissions.
- Restart the mobile application.

---

## Missing photographs

- Verify the dataset is mounted.
- Check ZFS snapshots.
- Review Immich logs.

---

## Performance issues

- Verify SSD application storage.
- Monitor CPU and memory usage.
- Confirm database health.

---

# Lessons Learned

Deploying Immich reinforced several infrastructure principles:

- Personal photographs require stronger backup policies than media libraries.
- Separating application data from media simplifies recovery.
- Daily snapshots provide excellent protection against accidental deletion.
- Local ownership removes reliance on third-party cloud providers.

---

# Future Improvements

Planned enhancements:

- HTTPS
- Reverse proxy
- Automatic off-site backup
- Grafana monitoring
- AI feature evaluation

---

# Design Philosophy

Immich is one of the most critical services in the home lab.

Unlike movies and television shows, personal photographs cannot easily be replaced.

For this reason, backup, snapshot and recovery strategies prioritise the Immich dataset above almost every other application.