# Self-Hosted Media Server

A Docker-based self-hosted media server designed to automate media acquisition, organization, and streaming. This repository contains Docker Compose configurations for deploying and managing a collection of popular media management and supporting services in a centralized environment.

## Features

- **VPN Integration:** Routes supported application traffic through Gluetun for enhanced network privacy and security.
- **BitTorrent and Usenet Support:** Uses qBittorrent and SABnzbd for managing downloads.
- **Automated Media Management:** Radarr, Sonarr, and Bazarr handle movie, television, and subtitle management.
- **Indexer Management:** Prowlarr provides centralized indexer configuration and integration.
- **Media Requests:** Overseerr allows users to browse and request movies and television shows.
- **Plex Monitoring:** Tautulli provides usage statistics and monitoring for Plex.
- **Service Dashboard:** Heimdall provides a centralized dashboard for accessing services.
- **Container Log Management:** Dozzle offers a web-based interface for viewing Docker container logs.

## Installation

### 1. Prerequisites

Ensure the following requirements are met before proceeding:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- A VPN provider with WireGuard or OpenVPN support

### 2. Clone the Repository

Clone the repository and navigate to the project directory:

```bash
git clone https://github.com/syd-io/media-server.git
cd media-server
```

### 3. Configure Environment Variables

Create a local `.env` file using the provided example:

```bash
cp .env.example .env
```

Edit the `.env` file to match your environment and configuration requirements.

Example:

```ini
PUID=1000
PGID=1000
TIMEZONE=Asia/Singapore
WEBUI_PORT_QBITTORRENT=8081
```

Update the remaining variables as required, including VPN credentials, storage paths, and service-specific settings.

### 4. Deploy the Containers

Start all configured services in detached mode:

```bash
docker compose up -d
```

Docker Compose will download the required images and initialize the containers.

### 5. Access the Services

Once deployment is complete, the services can be accessed through the following local URLs:

| Service | Description | URL |
|---|---|---|
| **qBittorrent** | BitTorrent download client | `http://localhost:8081` |
| **Radarr** | Movie management | `http://localhost:7878` |
| **Sonarr** | Television show management | `http://localhost:8989` |
| **Bazarr** | Subtitle management | `http://localhost:6767` |
| **Heimdall** | Service dashboard | `http://localhost:80` |
| **Overseerr** | Media request management | `http://localhost:5055` |
| **Tautulli** | Plex monitoring and analytics | `http://localhost:8181` |
| **SABnzbd** | Usenet download client | `http://localhost:8080` |
| **Prowlarr** | Indexer management | `http://localhost:9696` |
| **Flaresolverr** | Automated challenge resolution | No Web UI |
| **Recyclarr** | Sonarr and Radarr configuration synchronization | No Web UI |
| **Dozzle** | Docker container log viewer | `http://localhost:8080` |

**Note:** Replace `localhost` with your server's IP address when accessing the services from another device on your network.

Verify the configured port mappings in your Docker Compose files before accessing the services. Ensure that no two services are assigned the same host port.

## Configuration

Service-specific configuration files are stored in the `configs/` directory.

The following configuration areas may need to be customized:

- **Environment Variables:** Configure user IDs, group IDs, timezone, application ports, and VPN credentials in `.env`.
- **Storage:** Configure persistent volumes for application data and media libraries.
- **Media Paths:** Mount your media storage directory to `/data` inside the relevant containers.
- **Network:** Review Docker networking and VPN routing configurations to ensure that supported services use the intended network path.

## Maintenance

The following commands can be used to manage and maintain the deployment.

**View container logs:**

```bash
docker compose logs -f
```

**View logs for a specific service:**

```bash
docker compose logs -f <service>
```

**Restart a specific service:**

```bash
docker compose restart <service>
```

**Stop all services:**

```bash
docker compose down
```

**Update container images and recreate services:**

```bash
docker compose pull
docker compose up -d
```

## Security Considerations

- Keep VPN credentials and other sensitive configuration values in the `.env` file.
- Do not commit `.env` files or credentials to version control.
- Restrict access to service web interfaces, particularly when exposing them outside your local network.
- Regularly update Docker images and application configurations.
- Verify VPN connectivity and routing to ensure that designated download traffic does not bypass the VPN.

## License

This project is licensed under the [MIT License](https://opensource.org/license/mit/).
