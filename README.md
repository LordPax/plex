# Plex

## Description

Docker container for Plex Media Server.

## Service

- [Plex](http://localhost:32400/web)
- [Radarr](http://localhost:7878)
- [Sonarr](http://localhost:8989)
- [Prowlarr](http://localhost:9696)
- [Transmission with openvpn](http://localhost:9091)
- [Overseerr](http://localhost:5055)

## Configuration

### Environment Variables

rename `.env.example` to `.env` and set the variables

```
DATA_PATH=./dist
CONTAINER_PATH=./dist/container
TIMEZONE=Europe/Paris
PLEX_CLAIM=

OPENVPN_PROVIDER=PIA
OPENVPN_CONFIG=switzerland
OPENVPN_USERNAME=user
OPENVPN_PASSWORD=password
OPENVPN_LOCAL_NETWORK=192.168.1.0/16
```

## Usage

```bash
docker compose up -d
```
