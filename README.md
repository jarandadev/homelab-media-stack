# Media Stack (Jellyfin + Servarr + Docker)

A high-performance, automated media ecosystem for **discovery, acquisition, organization, and streaming**. Built on Docker, this stack provides a seamless "request-to-watch" workflow with zero manual file intervention.

---

## 🧩 Services Overview

| Service | Purpose | Port |
|-------|------|------|
| **Jellyfin** | Media server & web player | `8096` |
| **Jellyseerr** | User request & discovery portal | `5055` |
| **Prowlarr** | Indexer manager (Syncs to Radarr/Sonarr) | `9696` |
| **Radarr** | Movie collection management | `7878` |
| **Sonarr** | TV series collection management | `8989` |
| **Bazarr** | Automated subtitle downloader | `6767` |
| **qBittorrent** | BitTorrent client | `8080` |

---

## 📂 Directory Structure

To enable **Hardlinks** and **Atomic Moves**, everything under `/data` **must live on the same filesystem**.

```
.
├── docker-compose.yml
├── .env
├── config/                 # Persistent container configuration
└── data/                   # Persistent data
    ├── media/
    │   ├── movies/
    │   └── tv/
    └── torrents/           # Active downloads and seeding
```

---


## 🚀 Quick Start

### 1. Prerequisites
Ensure you have Docker and Docker Compose installed. You will also need to know your user ID (PUID) and group ID (PGID) to avoid permission issues.
```bash
id $USER
```

### 2. Installation
```bash
# Clone the repository
git clone https://github.com/jarandadev/homelab-media-stack
cd homelab-media-stack

# Create required directories
mkdir -p data/{torrents,media/{movies,tv}} config/{jellyfin,qbittorrent,prowlarr,radarr,sonarr,bazarr,jellyseerr}

# Configure environment
cp .env.example .env
nano .env
```

### 3. Deployment
```bash
docker-compose up -d
```
Access services via `http://<host>:<port>`.

---

## 🛠️ Maintenance
### Update all services:
```bash
docker compose pull
docker compose up -d --remove-orphans
```
### View Logs:
```bash
docker compose logs -f [service_name]
```