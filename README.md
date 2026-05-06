# PROIECT DRACULA — Technical Manifesto

> *"The network is not a utility. It is a weapon. We chose to wield it."*

## Overview

**Proiect Dracula** is a 5-week field engineering project documenting the design, failure, and ultimate success of building a sovereign home infrastructure from scratch on a Raspberry Pi 5 — without surrendering control to ISP hardware, cloud lock-in, or consumer-grade limitations.

This repository contains the live Command Center dashboard hosted at [thehandpi.org](https://thehandpi.org).

---

## The Architecture

| Node | Role | IP |
|------|------|----|
| **DRACULA** | The Architect / Primary Workstation | — |
| **DRACU** | Secondary Node | — |
| **DRACULAPI** | The Hand — Raspberry Pi 5 (Server) | 192.168.1.10 |
| **UGREEN NAS** | The Vault — 14TB Long-Term Storage | 192.168.1.25 |
| **4TB Toshiba** | Working Memory (being migrated) | — |
| **Samsung** | Mobile Node | 192.168.1.200 |

---

## The 5-Week Engineering Log

### Week 1 — The ISP Lockout & The "Boss" Hierarchy
The T-Mobile gateway firmware blocked advanced configuration. We demoted it to a Layer 2 Pipe and promoted the TP-Link Archer A54 to **Access Router (AR / Router Boss)**, unifying the entire 192.168.1.x subnet under our control.

### Week 2 — The 443GB Bug & The Storage Horizon
Default SMB mounts hallucinated a 443GB ceiling on the 14TB UGREEN NAS. Root cause: missing `noserverino` flag causing inode collisions. Fix: SMB v3.0 with `noserverino`, `vers=3.0`, `cache=none` in `/etc/fstab`. **13.5TB unlocked.**

### Week 3 — Docker Stability & The Database Migration
MariaDB on the Pi's SD card triggered Exit Code 139 (segfault) crash loops under I/O load. Migrated all Docker volumes — Nextcloud, MariaDB, Uptime Kuma — to the 14TB Vault. **100% uptime achieved. 119,274 files indexed.**

### Week 4 — Native AI Integration & Zero-Trust Ingress
Containerized AI (OpenClaw) failed due to volume binding conflicts. Replaced with **Claude Code CLI** (Node 22) for native POSIX filesystem control. Deployed **Cloudflare Zero Trust Tunnel** — zero open ingress ports, full external access.

### Week 5 — Legacy Migration & Cross-Device Sync
Initiated full migration of the 4TB Toshiba "swamp" to the organized 14TB Vault via parallel rsync (4 workers). Nextcloud syncs the Samsung phone and all laptops in real time. **Data consolidation active.**

---

## Service Stack

| Service | Port | Status |
|---------|------|--------|
| Nextcloud | :8080 | Active |
| MariaDB | :3306 | Active |
| Pi-hole DNS | :53 / :8053 | Active |
| Uptime Kuma | :3001 | Active |
| Home Assistant | :8123 | Active |
| CUPS Print Server | :631 | Active |
| Cloudflare Tunnel | — | Active |

---

## Security Posture

- **Zero open ingress ports** on the edge router
- **Cloudflare Zero Trust** tunnel for external access
- **Pi-hole** blocking ads and malicious domains network-wide
- **SMB v3.0** with hardened fstab flags
- All services containerized with restart policies

---

### Project Lead: Dracula

Built on a Raspberry Pi 5 | May 2026  
Accountability Ledger: $482.00  
*"From chaos, a protocol."*
