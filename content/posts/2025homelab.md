---
title: "2025 Homelab"
date: 2025-05-23T17:36:09-04:00
slug: 2025-05-23-2025homelab
type: posts
draft: true
categories:
  - projects
tags:
  - homelab
  - server
---

# important stuff
- Specs:
	- CPU: INTEL i7-6700K
	- COOLER: Cooler Master Hyper 212 Black Edition
	- RAM: Vengenance LPX DDR4 2400 MHz (8 GB x 2)
	- MOBO: ASUS Z170-A
	- PSU: Corsair RM 550x
	- CASE: Cooler Master N400
	- STORAGE: WD Black NVMe 1TB SSD + 5x 4TB WD Red + 2x 10TB WD Red Pro
	- GPU: Intel ARC A310
- OS:
	- TrueNas Scale - Electric Eel

- Services:
	- Calibre - Ebook management
	- Kavita - Webbased ereader
	- Immich - Photo backup
	- Jellyfin - Media Server
	- TailScale - VPN
	- qBittorrent - Torrent client with Gluetun vpn client
	- Paperless-ngx - document manager
	- Nginx proxy manager - reverse proxy manager
	- Homepage - dashboard
	- Watchtower - docker container updater
	- Audiobookshelf - audiobook client
	- Sonarr - Show indexer/PVR
	- Radarr - movie indexer/PVR
	- Prowler - indexer

	
# the story
- during covid, youtube recommended a video about home servers to me and I instantly i was hooked
- I've always been a privacy focused guy and loved the idea of having control of the media i used 
	- the home server became the next evolution of that
- my friend was upgrading his computer so I was able to get some cheap components to start
- I had to buy the case, power supply, storage and cooler 
- know literally nothing, I started by following hardware haven's tutorials (link)
	- set up with proxmox and truenas core
	- used it for mainly media content and backing up photos manually on the file system using photosync
	- **insert og photo**

- I moved back to my university city after moving I was getting a bios error, getting busy with school and let the computer sit for about a year and half
- i decided enough time had passed and i would try to get it running again
	- literally all I needed to do was update the bios - took 30 mins to do
- with starting it back up, I thought it would be nice to revamp it
	- things I wanted to change:
		- change from proxmox + truenas core to just truenas scale
			- rational - the vms are unnecessary cause i can run all the services i need through truenas scale  
		- add an hba
-  I got the LSI 9207-8i, installed truenas scale
-  I had about 2 weeks of trial and error setting up the services butt i got somewhere functional and happy
- ive replaced the gpu for intel arc a310
- **insert new photo**