# Plex

## Description

Docker container for Plex Media Server.

## Service

- [Plex](http://localhost:32400/web) - for media streaming
- [Radarr](http://localhost:7878) - for movies downloads
- [Sonarr](http://localhost:8989) - for tv shows downloads
- [Bazarr](http://localhost:6767) - for subtitles
- [Prowlarr](http://localhost:9696) - for indexers management
- [Transmission with openvpn](http://localhost:9091) - for torrents downloads
- [Overseerr](http://localhost:5055) - for requests

## Steps

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
OPENVPN_LOCAL_NETWORK=192.168.1.0/24
```

### Dns

Add dns `1.1.1.1` to `/etc/systemd/resolved.conf` or `/etc/resolv.conf` if needed

* /etc/systemd/resolved.conf (if systemd-resolved is enabled)

```bash
DNS=1.1.1.1
```

* /etc/resolv.conf (not persistent)

```bash
nameserver 1.1.1.1
```

### Kernel Modules

Run lsmod to check if the tun module is loaded

```bash
lsmod | grep tun
```

If the module is not loaded, you can load it with the following command

```bash
sudo modprobe tun
```

Create file `/etc/modules-load.d/tun.conf` with the following content to load the module at boot

```
tun
```

### Permissions

Set the permissions for the data folder

```bash
sudo chown -R 1000:1000 $DATA_PATH
mkdir $DATA_PATH/downloads/{complete,incomplete}
```

### Run the service

```bash
docker compose up -d
```
