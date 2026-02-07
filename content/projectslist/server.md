---
title: "Home Server"
date: 2022-12-27T22:29:18-05:00
draft: false
type: page
---

Completed: January 2022

Since I've been into computers the idea of making a NAS was on my radar, but never saw the use of it until I got around to starting a media server using my laptop. Space started filling up quickly and the idea of a home lab server came up again. At the same time, one of my friends upgraded a bunch of his computer and he wanted to sell parts for cheap. Everything lined up so I decided I would build my own server.

Here are the components I'm working with:
- CPU: INTEL i7-6700K
- COOLER: Cooler Master Hyper 212 Black Edition
- RAM: Vengenance LPX DDR4 2400 MHz [8 GB x 2]
- MOBO: ASUS Z170-A
- PSU: Corsair RM 550x
- CASE: Cooler Master N400
- STORAGE: WD Black NVMe SSD [1 TB] + 4 x WD Red [4 TB]

I am using Proxmox as my virtualization management system. Within Proxmox, I'm running 2 virtual machines:
1. TrueNAS - my NAS
2. Windows - to run some services
    1. Jellyfin - media server
    2. qBittorrent - torrent client
    3. Sonarr - internet PVR
    4. Prowlarr - indexer
    5. PhotoSync - backup for photos on phone

With this, I tried to passthrough a GTX 1070 to the Windows VM, but I could not get past the error 43. I may come back to this in the future. Eventually, I would also like to set up a VPN to allow me to remote into my services outside of my home network. I've been using the server for about a week now, it's been  awesome. It's nice having all of this storage avaiable to all of my devices and Jellyfin has made media consumption effortless.  




