---
title: "Setting up your own music server"
date: 2025-07-17T21:23:12-04:00
slug: 2025-07-17-music-server
type: posts
draft: false
tags:
  - homelab
  - guides
  - music
---

# Overview
We live in an age of software as a service (SaaS). For a monthly fee, these software give their users access to the conveniences of their product. Services like Netflix and Spotify give their users access to petabytes of content without the struggle of hosting or carrying that content themselves. The convenience is undeniable, but not without their concerns. Focusing on Spotify, their revenue stream for their artists isn't small artist friendly, mainly benefitting labels and popular artists. Nothing wrong with convenience, but if you are looking to support artist, you are better off buying the artists music directly and listening to the files off your phone. Unfortunately, given a large enough collection, it is not feasible to save thousands of songs along with photos and apps on a phone anymore. There is the option of getting a dedicated music player like an iPod or music player, but that poses its own inconveniences. The goal is to have something almost as accessible as Spotify, and with selfhosting it is now possible. This post will go over the steps to create your own music service using Navidrome as the music server. To track your listening, this will also show you how to connect Navidrome to Last.fm. 

With this tutorial, the service will only be accesible on your home network. To access it on the go, you will either have to set up a VPN to you home network, using a mesh network like TailScale or Twingate, or forward the port to the internet. This tutorial does not go into those steps. 

# Prerequisites
To create your own music service you will need the following:
- Server or a pc that is on all the time
	- I personally run everything on my NAS via TrueNAS Scale 
- [Navidrome](https://www.navidrome.org/) - the music server
- Optional: For listening statistics, Navidrome can send scrobble stats to other services:
	- [Last.fm](https://www.last.fm/home) - with an account

# Disclaimer:
- This is not a tutorial for piracy. Make sure to acquire your music through legal means, either through purchasing the digital files or ripping a CD.

Steps:
1. Install Navidrome on your setup. There is a couple methods to do this:
	- Docker - whether on Windows, Linux or a Homelab, docker is probably the easiest set up method. I installed the program using the TrueNAS Scale community app on my server
	- There is also the option of installing via YAML. As of this this tutorial, the yaml is found below (check the source for the up to date one. The community app on TrueNAS only requires you to set your volumes, so along with that make sure your user permissions are set properly as per your docker install.
	- There is a windows install for Navidrome but I haven't used it so I can't speak to its install process
```yaml
services:
  navidrome:
    image: deluan/navidrome:latest
    user: 1000:1000 # should be owner of volumes
    ports:
      - "4533:4533"
    restart: unless-stopped
    environment:
      # Optional: put your config options customization here. Examples:
      # ND_LOGLEVEL: debug
    volumes:
      - "/path/to/data:/data"
      - "/path/to/your/music/folder:/music:ro"
```

2. Once Navidrome is installed, access the webapp using http://yourip:4533 (replace the port if you changed it for your install) create your admin accounts as well as any users needed
3. If you pointed the music folder in the install to your music folder, then it should starting scanning automatically and you should see it shortly. Otherwise. move your music files over to the navidrome music folder.

And thats it! The main steps are done. The following is optional steps to add scrobbling for music tracking:

To add Last.fm (following this [Source Documentation](https://www.last.fm/api/account/create):
1. Create a Last.fm account/Login to your account
2. Create an API key for your navidrome instance. You only need to fill in the application name and the rest can be blank
3. In your navidrome data folder (the folder you made for your docker install), create a file called "navidrome.toml", this is where you will put any configuration/api information
4. Open the toml file in a text editor and add your parameters below using your API and secret key (don't forget the quotations, those are needed):
```yaml
LastFM.ApiKey = "your api key"
LastFM.Secret = "your secret key"
```
5. Login into the user you want to scrobble, then click on your profile icon on the top right, select Personal, and then on that page select Scrobble to Last.fm

{{< figure
  src="/images/navidrome-post/personal.png"
  alt="A menu screen"
  caption="This is what the menu looks like with the enable scrobble button at the bottom"
  class="ma0 w-75"
  width=125%
>}}  