# Media Server

## Description

Docker container for media management and automation. This repo includes Radarr, Sonarr, Bazarr, Prowlarr, Transmission, Jellyfin and Ombi for a complete media downloading, organization and streaming solution.

## Service

- [Jellyfin](http://localhost:8096/web) - for media streaming
- [Radarr](http://localhost:7878) - for movies filter and search on indexers
- [Sonarr](http://localhost:8989) - for tv shows filter and search on indexers
- [Lidarr](http://localhost:8686) - for music filter and search on indexers
- [Readarr](http://localhost:8787) - for books filter and search on indexers
- [Prowlarr](http://localhost:9696) - for indexers management
- [Transmission](http://localhost:9091) - for torrents downloads
- [Ombi](http://localhost:3579) - for requests management

## Steps

### Environment Variables

rename `.env.example` to `.env` and set the variables

```
DATA_PATH=./dist
CONTAINER_PATH=./dist/container
TIMEZONE=Europe/Paris
DOMAIN=

OPENVPN_PROVIDER=PIA
OPENVPN_CONFIG=switzerland
OPENVPN_USERNAME=user
OPENVPN_PASSWORD=password
OPENVPN_LOCAL_NETWORK=192.168.1.0/24

TRANSMISSION_USERNAME=
TRANSMISSION_PASSWORD=
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

### Run the service

Run to generate the configuration files

```bash
docker compose up -d
```

### Permissions

Set the permissions for the data folder (replace DATA_PATH with the path in the .env file)

```bash
sudo chown -R 1000:1000 DATA_PATH
mkdir DATA_PATH/downloads/{completed,incomplete}
```

### SSL Certificates

Add the SSL certificates to the `CONTAINER_PATH/nginx/certs` folder, file must have same name as your domain (replace CONTAINER_PATH with the path in the .env file)

```
CONTAINER_PATH/nginx/certs/domain.com.crt
CONTAINER_PATH/nginx/certs/domain.com.key
```

### Restart the service

```bash
docker compose restart
```
