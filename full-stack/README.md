
# Full-Stack Media Automation Stack

This project uses Docker Compose to orchestrate a suite of media management, automation, and enhancement services. Services are grouped by their primary function:

## 1. Plex & Plex Request
- **plex**: The core Plex Media Server for streaming and library management.
- **plex_request**: Manages media requests for Plex users.
- **plex_request_nginx**: Nginx reverse proxy for Plex request service.
- **plex_authentication**: Handles authentication for Plex-related services.
- **plex-recommendations**: AI-powered recommendations for Plex, using OpenAI and Plex APIs.
- **tautulli**: Plex usage and activity monitoring and analytics.
- **overseerr**: User-friendly media request and management system for Plex.
- **plextraktsync**: Syncs Plex watch history and ratings with Trakt.tv.

## 2. Arr Stack + Gluetun + Rclone
- **radarr**: Movie collection manager for Usenet and BitTorrent users.
- **sonarr**: TV series collection manager for Usenet and BitTorrent users.
- **prowlarr**: Indexer manager and proxy for Radarr, Sonarr, and other *arr apps.
- **decypharr**: Handles decryption and blackhole management for downloads.
- **tweakio**: Additional media automation and management tool.
- **gluetun**: VPN client container, provides network privacy for dependent services.
- **rclone**: Mounts and manages cloud storage for media files.

## 3. Scraping
- **kometa**: Automates Plex metadata and collection management.
- **huntarr**: Searches for missing or wanted media content.

## 4. Repair & Maintenance
- **rescan**: Triggers rescans of Plex libraries to keep them up to date.
- **autoscan**: Listens for file changes and triggers Plex library scans.
- **decluttarr**: Cleans up and manages media libraries by removing failed, missing, or orphaned items. Integrates with Radarr and Sonarr.

## Networking
All services are connected via a shared Docker network (`arr`), with some services using `network_mode: service:gluetun` for VPN routing.

## Volumes & Configuration
- Most services use environment variables for configuration, with secrets and paths provided via a `.env` file.
- Persistent data and configuration are stored in mapped volumes under `${CONFIG_BASE}` and `${MOUNT_PATH}`.

## Dependencies
- Many services depend on `plex` and/or each other for correct startup order.
- Some services (e.g., `radarr`, `sonarr`, `prowlarr`, `decypharr`, `tweakio`) require the VPN (`gluetun`) and cloud mount (`rclone`) to be healthy before starting.

---

**Note:**
- Update the `.env` file with your environment-specific values before deploying.
- For more details on each service, refer to their respective documentation.
