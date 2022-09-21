# Automated Media Server

Simple home media server, using Plex, with automated syncing of your favorite movies, tv shows, and music. Powered by Docker.

All downloads will be encrypted and secured through a VPN, to prevent any prying eyes on your local network or ISP from monitoring what you download. All of this will be powered with simple Docker containers, meaining there is no need to install and configure what tends to be complex software.

*In no way am I recommending or endorsing downloading illegal content. You are responsible to know and follow the laws in your area.*

## Description of media server and services

* Plex - This will serve the audio and video files. Plex has client apps for nearly any device on which you would want to play media.
* OpenVPN client container - This container will supply the secure tunnel for encrypted downloads. It will hide your traffic from prying eyes.
* SABnzbd - Usenet file downloader.
* Prowlarr - Usenet index manager. This keeps the indexers in sync, across all services.
* Sonarr - TV show management. Sonarr actively searches the indexes for new and existing shows of your choice.
* Radarr - Movie management. Radarr actively searches the index for new and existing movies of your choice. 
* Lidarr - Music management. Lidarr actively searches the indexes for new and existing music of your choice.

For additional documentation and details on the *arr services, see [https://wiki.servarr.com](https://wiki.servarr.com).

This is not an exhaustive list of media management servers, but is a representation of what I have tested and found to work well.
Will a little digging, you can also find services for ebooks, audible books, comic books, software, and more.

## Get started

### Ports quick list

### Prerequisites

* An openvpn compatible VPN service. 
* Working Docker and docker-compose.
* Access to the `ovpn` files from your VPN service. These can be found through documentation or contacting support.
* Usenet account for downloading
* Usenet index account

*Note:* This setup uses SABnzbd for downloading, however the download client can be swapped out for torrents or another service.

### Setup

Simplicity has been kept in mind for this setup. As such the setup steps have been kept to the absolute minimum.

* Clone or download this repository.
* Place the `ovpn` and related files into the `vpn/` folder.
* Rename the `.env.example` file to `.env`.
* Edit the `.env` file and update your settings. See the [Environment variables](#environment-variables) section below.
* Start it up with `docker-compose up -d && docker-compose logs -f`.

*Note:* The Docker containers should not run interactively. Be sure to configure your VPN service to authenticate automagically.

### Environment variables

The following environment variables are available for configuring.

| Variable | Example| Description |
| --- | --- | --- |
| PUID | `1000` | Host user ID to run the container as. |
| PGUID | `1000` | Host user's group id to run the container as. |
| TZ | `America/Los_Angeles` | Timezone for the server to work in. |
| MEDIA `/mnt/media` | Root location of media files. |
| DOWNLOADS | `/media/downloads` | Location of incomplete downloads. |
| PLEX_UID | `1000` | Host user ID to run the Plex as. |
| PLEX_GID | `1000` | Host user's group id to run Plex as. |
| HOSTNAME | `My Media Server` | Plex server name. |
| PLEX_CLAIM | | Plex claim. |
| VPN_CONFIG_FILE | | The `ovpn` file to load from the `vpn/` folder. |
| SUBNETS | `192.168.0.0/24` | Local network subnet. | 

## VPN services that have tested well.

Any openvpn compatible VPN service should work, however the following is a list of VPN services that have tested well.

* [TunnelBear](https://www.tunnelbear.com)
* [Private Internet Access (PIA)](https://www.privateinternetaccess.com)

There are [many resources available](http://duckduckgo.com/?q=fastest+vpn+service) to help you find a fast VPN service that is right for you.

Note: Download speed through a VPN may be significantly slowerthat your actual connection. This is due to the networking overhead and the speed of the VPN servers. Do not expect to download with the same speed you would without the VPN.

## Issues, questions, and troubleshooting

Found an issue? Have a question? [Create a ticket](https://github.com/blobaugh/docker-media-server/issues)
