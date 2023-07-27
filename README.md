# Homelab

I run my media server and the sort of "management" side as a collection of docker containers. What follows is a list and short instructions for each to get them set up for yourself.

Requirements:

- **VPN** Might not be neccessary, but I use one for peace of mind.

- **Discord server** to set up notifications from some of the services

- **Domain** (dynamic one works fine) to access jellyfin and audiobookshelf from external devices.

Getting it all up and running:

- Clone repo

        git clone https://github.com/Hoopaugi/Homelab.git

- Create `.env` file according to `example.env` in the directory root

- Follow instructions on the Nordlynx section to acquire the private key for the vpn and set it in the `.env` file.

- Start services

        docker compose up -d

- Follow instructions for each service in their own sections. Suggested order of configuration:

1. **Pihole** to get local DNS and domain working
2. **qBittorrent** Has to be added to some of the following services. Also verify that the vpn is working with [IPLeak](https://ipleak.net/)
3. **Lidarr, Radarr, Readarr & Sonarr** Skip indexer configuration.
4. **Prowlarr** To set up and sync indexers to the above
5. **Audiobookshelf & Jellyfin** To configure your media streaming services
6. **Grafana** To set up nice graphs
7. **Uptime-Kuma** To set up notifications about service health

- Each service can be accessed from the browser via `<server ip>:<service port>`, and with `<service name>.homelab` after pihole has been configured.

## Management Services

### Dashy

> Dashy is an open source, highly customizable, easy to use, privacy-respecting dashboard app.

[dashy.to](https://dashy.to/) | [Docker Hub](https://hub.docker.com/r/lissy93/dashy) | [Github](https://github.com/Lissy93/dashy)

### Grafana

> Grafana is a multi-platform open source analytics and interactive visualization web application.

[Grafana.com](https://grafana.com/) | [Docker Hub](https://hub.docker.com/r/grafana/grafana)

### Pihole

> Pi-hole is a Linux network-level advertisement and Internet tracker blocking application which acts as a DNS sinkhole and optionally a DHCP server

Uses cloudflared for DNS resolution by default. This can be changed in the web interface, or in the compose file by changing the `PIHOLE_DNS_` environmental variable.

In the web interface, under `Local DNS` => `DNS Records`, create a new record for each of the services pointing to the IP address of your server. These records should follow the pattern `<service name>.homelab`, for example `pihole.homelab`

[Pi-hole.net](https://pi-hole.net/) | [Docker Hub](https://hub.docker.com/r/pihole/pihole) | [Github](https://github.com/pi-hole/docker-pi-hole)

### Prometheus

> An open-source monitoring system with a dimensional data model, flexible query language, efficient time series database and modern alerting approach.

Create a config file `prometheus.yml` in the config folder according to the `example.prometheus.yml` file

[prometheus.io](https://prometheus.io/) | [Docker Hub](https://hub.docker.com/r/prom/prometheus/) | [Github](https://github.com/prometheus/prometheus/)

### Traefik

> Traefik is a leading modern reverse proxy and load balancer that makes deploying microservices easy.

[traefik.io](https://traefik.io/traefik/) | [Docker Hub](https://hub.docker.com/_/traefik) | [Github](https://github.com/traefik/traefik-library-image)

### Uptime-Kuma

> Uptime Kuma is an easy-to-use self-hosted monitoring tool.

Create a new monitor for each of the services you are running, and set up notifications via a discord webhook

[uptime.kuma.pet](https://uptime.kuma.pet/) | [Docker Hub](https://hub.docker.com/r/louislam/uptime-kuma) | [Github](https://github.com/louislam/uptime-kuma)

### Watchtower

> A container-based solution for automating Docker container base image updates.

[containrrr.dev](https://containrrr.dev/watchtower/) | [Docker Hub](https://hub.docker.com/r/containrrr/watchtower) | [Github](https://github.com/containrrr/watchtower)

## Media Services

Pretty much just the common -arr stack

### Audiobookshelf

> Self-hosted audiobook and podcast server.

If you want access via the android client, you will have to do some port forwarding, and to have a domain.

[audiobookshelf.org](https://www.audiobookshelf.org/) | [Docker Hub](https://hub.docker.com/r/advplyr/audiobookshelf) | [Github](https://github.com/advplyr/audiobookshelf)

### Flaresolverr

> FlareSolverr is a proxy server to bypass Cloudflare and DDoS-GUARD protection.

[Docker Hub](https://hub.docker.com/r/flaresolverr/flaresolverr) | [Github](https://github.com/FlareSolverr/FlareSolverr)

### Jellyfin

> Jellyfin is a free and open-source media server and suite of multimedia applications designed to organize, manage, and share digital media files to networked devices.

To access from external networks, you will have to port forward and have a domain.

[jellyfin.org](https://jellyfin.org/) | [Docker Hub](https://hub.docker.com/r/linuxserver/jellyfin) | [Github](https://github.com/linuxserver/docker-jellyfin)

### Jellyseerr

> Jellyseerr is a free and open source software application for managing requests for your media library.

[Docker Hub](https://hub.docker.com/r/fallenbagel/jellyseerr) | [Github](https://github.com/Fallenbagel/jellyseerr)

### Lidarr

> Lidarr is a music collection manager for Usenet and BitTorrent users.

Go through the settings, skipping indexer setup, as the indexers are managed by prowlarr.

[lidarr.audio](https://lidarr.audio/) | [Docker Hub](https://hub.docker.com/r/linuxserver/lidarr) | [Github](https://github.com/linuxserver/docker-lidarr)

### Nordlynx

> NordVPN is a VPN service

[nordvpn.com](https://nordvpn.com/) | [Docker Hub](https://hub.docker.com/r/bubuntux/nordlynx) | [Github](https://github.com/bubuntux/nordlynx)

To generate the private key:

- Follow these [instructions](https://support.nordvpn.com/Connectivity/Linux/1905092252/How-to-log-in-to-NordVPN-on-Linux-with-a-token.htm) to generate a token

- Using the token, run the following container to generate the key

        docker run --rm --cap-add=NET_ADMIN -e TOKEN=<Your token here> bubuntux/nordvpn:get_private_key

### Prowlarr

> Prowlarr is an indexer manager/proxy built on the popular *arr .net/reactjs base stack to integrate with your various PVR apps.

Go through the settings, add Lidarr, Radarr, Readarr and Sonarr in the Apps, configure the indexers you want to use and sync them to the services.

[prowlarr.com](https://prowlarr.com/) | [Docker Hub](https://hub.docker.com/r/linuxserver/prowlarr) | [Github](https://github.com/linuxserver/docker-prowlarr)

### qBittorrent

> qBittorrent is a cross-platform free and open-source BitTorrent client

Go through the options. I recommend setting up seperate default save and incomplete directories. To make importing and cleanup of torrents faster, set seeding ratio to 0 and the action to "pause torrent".

[qbittorrent.org](https://www.qbittorrent.org/) | [Docker Hub](https://hub.docker.com/r/linuxserver/qbittorrent) | [Github](https://github.com/linuxserver/docker-qbittorrent)

### Radarr

> Radarr is a movie collection manager for Usenet and BitTorrent users.

Go through the settings, skipping indexer setup, as the indexers are managed by prowlarr.

[radarr.video](https://radarr.video/) | [Docker Hub](https://hub.docker.com/r/linuxserver/radarr) | [Github](https://github.com/linuxserver/docker-radarr)

### Readarr

> Readarr is a ebook collection manager for Usenet and BitTorrent users.

Go through the settings, skipping indexer setup, as the indexers are managed by prowlarr.

[readarr.com](https://readarr.com/) | [Docker Hub](https://hub.docker.com/r/linuxserver/readarr) | [Github](https://github.com/linuxserver/docker-readarr)

### Sonarr

> Sonarr is an internet PVR for Usenet and Torrents.

Go through the settings, skipping indexer setup, as the indexers are managed by prowlarr.

[sonarr.tv](https://sonarr.tv/) | [Docker Hub](https://hub.docker.com/r/linuxserver/sonarr) | [Github](https://github.com/linuxserver/docker-sonarr)

## Other services

### Node Exporter

Provices statistics from the host system, imported into prometheus and shown in grafana

[Instructions from](https://developer.couchbase.com/tutorial-node-exporter-setup)

Download repo

        wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz

Create new user and group for the service

        sudo groupadd -f node_exporter

        sudo useradd -g node_exporter --no-create-home --shell /bin/false node_exporter

Unpack node_exporter and move it

        tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz

        sudo cp node_exporter-1.6.1.linux-amd64/node_exporter /usr/bin/

Set owner

        sudo chown node_exporter:node_exporter /usr/bin/node_exporter

Create the service file

        sudo nano /usr/lib/systemd/system/node_exporter.service

Service file:

        [Unit]
        Description=Node Exporter
        Documentation=https://prometheus.io/docs/guides/node-exporter/
        Wants=network-online.target
        After=network-online.target

        [Service]
        User=node_exporter
        Group=node_exporter
        Type=simple
        Restart=on-failure
        ExecStart=/usr/bin/node_exporter \
        --web.listen-address=:9200

        [Install]
        WantedBy=multi-user.target

Set permissions

        sudo chmod 664 /usr/lib/systemd/system/node_exporter.service

Start and enable the service

        sudo systemctl daemon-reload

        sudo systemctl start node_exporter

        sudo systemctl status node_exporter

        sudo systemctl enable node_exporter.service