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
- why a vpn is important when torrenting
- what is gluetun
- how to use gluetun

# Prerequisites 
- TrueNAS Scale (I installed this on Electric Eel)
- A VPN provider (I used Private Internet Access, but anything like ProtonVPN, NordVPN, etc will work)

# Instructions
1. Copy the yaml code below to a code editor or text editor. 
  - explain the rest of the code
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
      - /mnt/main-pool/app-configs/qbit-gluetun:/config
      - /mnt/tank/media/downloads/downloads:/downloads
    restart: unless-stopped
networks: {}
```

2. change the gluetun environment
3. deploy the container
  - login for qbit is in the log files
4. test using a torrenting ip checker