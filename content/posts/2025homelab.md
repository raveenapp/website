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
---

# The Important Stuff
- Specs:
	- CPU: INTEL i7-6700K
	- COOLER: Cooler Master Hyper 212 Black Edition
	- RAM: 32 GB Vengenance LPX DDR4 2400 MHz (8 GB x 4)
	- MOBO: ASUS Z170-A
	- PSU: Corsair RM 550x
	- CASE: Cooler Master N400
	- STORAGE: WD Black NVMe 1TB SSD + 5x 4TB WD Red + 2x 10TB WD Red Pro
	- GPU: Intel ARC A310
	- HBA: LSI 9207-8i
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

- Stats: 
	- Average Power: 94 W
	- Total storage: Pool 1 - "vault" - 10.64TiB, Pool 2 - "tank" - 9.01TiB
# The Background
I first learned about homelabs during covid when youtube recommended a video about home servers to me. At that point, it was just about media servers but instantly I was hooked. I've always been a privacy focused guy when it comes to the internet and its always been a struggle to balance the conviniences of internet and keep my data private. Using a home server for media and file storage seemed like natural progression of that. So when my friend was upgrading his computer, I was able to snag some cheap components off him to start the build. I had to buy the case, storage and cooler! I started with 4 4Tb drives for the setup.

I had no idea where to actually start so went down a major youtube university rabbit hole and found this walkthrough that I liked by Hardware Haven.

{{< youtube kbbnAQ0AQw2FUjAl >}}

Following the video, I build my first server using Proxmox and TrueNAS Core. I ran a vm of Windows 10 that ran my services like Jellyfin and I used PhotoSync to backup my photos on to the server. 

{{< figure
  src="/images/homelab-post/og-homelab.jpeg"
  alt="Picture of inside a computer"
  caption="This was the original setup, I tried using a 1070 for hardware acceleration, but I never got it to work"
  class="ma0 w-75"
  width=50%
>}}  

This worked fine but after a little while of use I realized it wasn't ideal. The Windows VM would crash often cause it would run out of ram so I'd constantly login in to Proxmox to restart it. But it would good enough and that was enough for me at that point. As the lockdowns were ramping down, I moved back to my university city. I took the server with me but I kept getting a startup error that I didn't recognize. I got busy with school and didn't make the time to try to troubleshoot the error so I let the system sit for a while. 

About 8 months ago, I thought enough time had passed and I should dedicate a day to fixing the server. After browsing some forums, it was just a BIOS error and all I needed was 30 mins to update the BIOS. After starting it up again, I went to through the same hurdles I went through before, so I thought it would be nice to revamp it!

I started researching some more, I decided that TrueNAS Scale would be a better OS than running Proxmox + TrueNAS Core for my usecase. I figured that the vm is unnecessary cause I can run all of the services I want via Docker through TrueNAS Scale anyway. I also wanted to order an HBA cause I was thinking of expanding my storage anyway and I was running out of SATA ports in my motherboard. I ordered the LSI 9207-8i from ArtofAServer on Ebay and in the meantime, I offloaded all of my data to a couple external harddrives I had lying around. 

Once the HBA came in, I installed it and TrueNAS Scale on baremetal, and remade my pool in RAIDZ1 and imported my data. After about 2 weeks of playing around with the services, I got back to where I was in the old server. While I was playing around with everything, I looked into the other apps that the TrueNAS Scale community catalogue had to offer and I was so impressed with what was available. 

I ended up upgrading my storage cause I didn't like the amount of redundancy I had, so now I have 2 pools. I have 5x 4TB of RAIDZ2 for all of my important files and then I have 2x 10 TB of MIRROR for all of my media. There is probably some ineffiencies in this set up but thats okay, it was something I wanted to experiment with. I also got an Intel ARC A310 for Jellyfin hardware encoding.

This is the new setup! 
{{< figure
  src="/images/homelab-post/homelabv2.jpeg"
  alt="Picture of inside a computer"
  caption="This is the new setup!"
  class="ma0 w-75"
  width=50%
>}}  


I will probably make some posts outlines how I set up some of the services I am running cause I found the documentation for those to be insufficent. You can click on the homelab to see more!