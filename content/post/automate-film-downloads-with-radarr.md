+++
author = "Josh Rickers"
categories = ["Radarr", "RuTorrent", "Automation", "Docker"]
date = 2018-06-06T21:27:51Z
description = ""
draft = false
slug = "automate-film-downloads-with-radarr"
tags = ["Radarr", "RuTorrent", "Automation", "Docker"]
title = "Automate Movie downloads with Radarr and RuTorrent"

+++


Another step on my home automation journey is finding a way to automate movie downloads and streaming. Since I already have Docker, RuTorrent and Jackett installed I can use a fork of Sonarr called Radarr.

## RuTorrent and Jackett
If you have come from my previous blog post then you will already have everything installed and ready to go. Jump to the Radarr section below.
If not take please take a look and you should find everything you need to get everything up and running - /automate-tv-shows-with-sonarr/
## Radar
Radarr is a fork of the popular TV automation program Sonarr. With a similar interface and setup it is the best solution to my movie automation problem.

We will be using Docker again as it is so useful. My set up also makes use of the Nginx and Let's Encrypt container - [see my other post](/docker-nginx-and-lets-encrypt/) for instructions on how to set this up.

Running the following command will set up the Radarr container with the correct settings. Make sure to modify the command to suit your setup and to create the relevant folders.

```
docker create --name=radarr -v /path/to/radarr/config:/config -v /path/to/rutorrent/downloads:/downloads -v /path/to/movies:/movies -v /etc/localtime:/etc/localtime:ro -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -p 7878:7878 linuxserver/radarr

```
Next run
```
docker start radarr
```
The Radarr container should spin up and visiting http://yourip:7878 should display Radarr.

You are now ready to configure Radarr and set up your automatic film downloads.

