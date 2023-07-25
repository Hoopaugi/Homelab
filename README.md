# Homelab

## Management Services

### Grafana

> Grafana is a multi-platform open source analytics and interactive visualization web application.

[Grafana.com](https://grafana.com/) | [Docker Hub](https://hub.docker.com/r/grafana/grafana)

### Pihole

> Pi-hole is a Linux network-level advertisement and Internet tracker blocking application which acts as a DNS sinkhole and optionally a DHCP server

[Pi-hole.net](https://pi-hole.net/) | [Docker Hub](https://hub.docker.com/r/pihole/pihole) | [Github](https://github.com/pi-hole/docker-pi-hole)

### Prometheus

> An open-source monitoring system with a dimensional data model, flexible query language, efficient time series database and modern alerting approach.

[prometheus.io](https://prometheus.io/) | [Docker Hub](https://hub.docker.com/r/prom/prometheus/) | [Github](https://github.com/prometheus/prometheus/)

### Traefik

> Traefik is a leading modern reverse proxy and load balancer that makes deploying microservices easy.

[traefik.io](https://traefik.io/traefik/) | [Docker Hub](https://hub.docker.com/_/traefik) | [Github](https://github.com/traefik/traefik-library-image)

### Uptime-Kuma

> Uptime Kuma is an easy-to-use self-hosted monitoring tool.

[uptime.kuma.pet](https://uptime.kuma.pet/) | [Docker Hub](https://hub.docker.com/r/louislam/uptime-kuma) | [Github](https://github.com/louislam/uptime-kuma)

### Watchtower

> A container-based solution for automating Docker container base image updates.

[containrrr.dev](https://containrrr.dev/watchtower/) | [Docker Hub](https://hub.docker.com/r/containrrr/watchtower) | [Github](https://github.com/containrrr/watchtower)

## Media Services

### Audiobookshelf

> Self-hosted audiobook and podcast server.

[audiobookshelf.org](https://www.audiobookshelf.org/) | [Docker Hub](https://hub.docker.com/r/advplyr/audiobookshelf) | [Github](https://github.com/advplyr/audiobookshelf)

### Jellyfin

> Jellyfin is a free and open-source media server and suite of multimedia applications designed to organize, manage, and share digital media files to networked devices.

[jellyfin.org](https://jellyfin.org/) | [Docker Hub](https://hub.docker.com/r/linuxserver/jellyfin) | [Github](https://github.com/linuxserver/docker-jellyfin)

### Lidarr

> Lidarr is a music collection manager for Usenet and BitTorrent users.

[lidarr.audio](https://lidarr.audio/) | [Docker Hub](https://hub.docker.com/r/linuxserver/lidarr) | [Github](https://github.com/linuxserver/docker-lidarr)

### Nordlynx

> NordVPN is a VPN service

[nordvpn.com](https://nordvpn.com/) | [Docker Hub](https://hub.docker.com/r/bubuntux/nordlynx) | [Github](https://github.com/bubuntux/nordlynx)

Generate private key

    docker run --rm --cap-add=NET_ADMIN -e TOKEN=XXX bubuntux/nordvpn:get_private_key

### Prowlarr

> Prowlarr is an indexer manager/proxy built on the popular *arr .net/reactjs base stack to integrate with your various PVR apps.

[prowlarr.com](https://prowlarr.com/) | [Docker Hub](https://hub.docker.com/r/linuxserver/prowlarr) | [Github](https://github.com/linuxserver/docker-prowlarr)

### qBittorrent

> qBittorrent is a cross-platform free and open-source BitTorrent client

[qbittorrent.org](https://www.qbittorrent.org/) | [Docker Hub](https://hub.docker.com/r/linuxserver/qbittorrent) | [Github](https://github.com/linuxserver/docker-qbittorrent)

### Radarr

> Radarr is a movie collection manager for Usenet and BitTorrent users.

[radarr.video](https://radarr.video/) | [Docker Hub](https://hub.docker.com/r/linuxserver/radarr) | [Github](https://github.com/linuxserver/docker-radarr)

### Readarr

> Readarr is a ebook collection manager for Usenet and BitTorrent users.

[readarr.com](https://readarr.com/) | [Docker Hub](https://hub.docker.com/r/linuxserver/readarr) | [Github](https://github.com/linuxserver/docker-readarr)

### Sonarr

> Sonarr is an internet PVR for Usenet and Torrents.

[sonarr.tv](https://sonarr.tv/) | [Docker Hub](https://hub.docker.com/r/linuxserver/sonarr) | [Github](https://github.com/linuxserver/docker-sonarr)
