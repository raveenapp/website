---
title: "How I set up qBittorrent with Gluetun on TrueNAS Scale"
date: 2025-05-29T07:51:59-04:00
slug: 2025-05-29-qbit-gluetun
type: posts
draft: true
categories:
  - projects
  - how-to
tags:
  - homelab
---

One thing that cause me a lot of trouble setting up was running qBittorent with a VPN on TrueNAS Scale. This is cause the community application of qBittorrent doesn't give you the option to edit the install file, so you will manually have to install it instead. 

# Overview
Regardless of what you want to torrent, its probably a good idea to run it through a VPN. It masks your IP address so that way it shouldn't be linked back to your usage. Typically, if you were torrenting on your computer, just turning on the VPN app and running it would be fine. But with servers that may run in the background, it is a little more complicated. Especially on something like TrueNAS which doesn't do the typical "installing applications" like on a computer. 

That is where Gluetun comes in. Gluetun is a VPN client that you can connect your docker containers to so traffic will pass through the VPN instead. There is two ways to connect to gluetun:
- First, running gluetun in its own stack. When you want to install an external container that feeds into gluetun, you'd add the following to that container:
  ``` yaml
    --network=container:gluetun
  ```
- Second, and what I did here is run Gluetun in the same docker-compose.yaml file as the other container:
  ``` yaml
    network_mode: "container:gluetun"
  ```

  The last thing to note is that there are 2 popular ways to install custom apps to TrueNAS Scale:
  - You can install via the TrueNAS GUI
  - Use a docker manager like Dockge or Portainer

In this tutorial, I will be installing Gluetun the same docker-compose.yaml and installing via Dockge, but the install method is transferable. 

(Link to Gluetun github repo)[https://github.com/qdm12/gluetun]

# Prerequisites 
- TrueNAS Scale (I installed this on Electric Eel)
- A VPN provider (I used Private Internet Access, but anything like ProtonVPN, NordVPN, etc will work)

# Instructions
1. In TrueNAS, create a dataset for your qBittorrent configs and make sure to set it as an app. You can name it whatever you'd like. For example, I have a config folder for my apps so it looks like /mnt/vault/app-configs/qbit-gluetun. You also need to make a folder for your torrents, this can be anywhere in your pool. In my case I have a separate pool for my media so it /mnt/tank/media/downloads.

2. Copy the yaml code at the bottom to a code editor or text editor. You will have to change the Gluetun environment variables based on your VPN provider. (https://github.com/qdm12/gluetun-wiki/tree/main/setup/providers). You will then have to modify the volumes so that /path/to/whatever: points to your config and download folders from step 1. In my case, they it would look like:
```yaml
    - /mnt/vault/app-configs/qbit-gluetun:/config
    - /mnt/tank/media/downloads:/downloads

```

3. That's it! You can start your container. If you haven't changed to ports, you should be able to connect to your qBittorrent webapp by typing your http://ip.address:8080. The initial log in information is in the log files and then you can change the signin credentials in your settings. 

4. The last step is to make sure its downloading correctly. You can google "torrent IP location tracker" or use the following (https://www.whatismyip.net/tools/torrent-ip-checker/index.php?hash=494c79ad127eac662ccbd0c55af4d98e2d08c2d0). Copy the magnet and download it on your qBittorrent client. Don't worry, it won't download any files. From the website, you can see what IP is being tracked and then just an IP location tracker to verify that it is not in the same country as your own. 


```yaml
version: "3"
services:
  gluetun:
    image: qmcgaw/gluetun
    container_name: gluetun
    cap_add:
      - NET_ADMIN
    ports:
      - 8080:8080/tcp
    environment:
      - VPN_SERVICE_PROVIDER=
      - OPENVPN_USER=
      - OPENVPN_PASSWORD=
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    environment:
      - PUID=568
      - PGID=568
      - TZ=Etc/EST
      - WEBUI_PORT=8080
      - TORRENTING_PORT=6881
    network_mode: service:gluetun
    volumes:
      - /path/to/config:/config
      - /path/to/downloads:/downloads
    restart: unless-stopped
networks: {}
```