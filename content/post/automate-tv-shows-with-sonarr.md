+++
author = "Josh Rickers"
categories = ["Sonarr", "Jackett", "Automation", "RuTorrent", "Docker"]
date = 2018-06-02T20:48:28Z
description = ""
draft = false
slug = "automate-tv-shows-with-sonarr"
tags = ["Sonarr", "Jackett", "Automation", "RuTorrent", "Docker"]
title = "Automate TV Shows with Sonarr, RuTorrent and Jackett"

+++


Automating things in my life is something that I have been trying to do for some time now. Quick and easy automation is what I look for, especially for media. Who doesn't like having the latest episodes at hand to just stream whenever you want? I know I do and Sonarr provides just that.

We are going to take a quick look at setting up Sonarr, RuTorrent and Jackett with our friend Docker.

## RuTorrent
RuTorrent is a gui for rTorrent, a torrent client available for Linux. I have been using RuTorrent for many years and running it through Docker is by far the most easiest way of setting it up.

[Linuxserver.io](https://hub.docker.com/u/linuxserver/) have a great selection of Docker containers and we are going to take full advantage of this.

Run the following command to set up the container making sure to create the RuTorrent directory first and changing the time zone and ports.
```
docker create --name=rutorrent -v /path/to/rutorrent/config:/config -v /path/to/rutorrent/downloads:/downloads -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -p 8686:80 -p 5000:5000 -p 51413:51413 -p 6881:6881/udp linuxserver/rutorrent
```
Then run
```
docker start rutorrent
```
Browse to http://yourip:8686 and you should see the RuTorrent gui. Check through some of the settings to make sure everything is how you want and you should be good to go.

## Jackett
Jacket is what we will be using to interface with torrent trackers. Sonarr does not handle this well on its own so we need Jacket to do a better job for us.

Again, we will be using a [linuxserver.io container](https://hub.docker.com/r/linuxserver/jackett/) for this.

Run the following command making sure to create the jackett directory first and changing the timezone.
``` 
docker create --name=jackett -v /path/to/jackett/config:/config -v /path/to/rutorrent/downloads:/downloads -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -v /etc/localtime:/etc/localtime:ro -p 9117:9117  linuxserver/jackett
```
Then run
```
docker start jackett
```

Browse to http://yourip:9117 and you will see the Jackett interface. Configuring Jackett is pretty straight forward.

## Sonarr
Sonarr will automate your TV show searches and downloads. I had previously used Sickrage but after starting a fresh server install I was looking for something a little bit more modern and I was suggested Sonarr.
Sonarr is mainly used with Usenet indexers but there is some basic functionality for Torrent sites. Jackett will treat Torrent sites like Usenet indexers and report back everything needed for many trackers.

As I mentioned above, we will be using a Docker container to run Sonarr. [linuxserver.io](https://hub.docker.com/u/linuxserver/) provide a nice and easy [Sonarr container](https://hub.docker.com/r/linuxserver/sonarr/). 

Create a Sonarr directory, a directory where you want to save your TV show and make note of where your downloads will be. For me this will be the location of my rutorrent downloads folder.

Run the following command to set everything up.

```
docker create --name sonarr -p 8989:8989 -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -v /etc/localtime:/etc/localtime:ro -v /path/to/sonarr/dir:/config -v /path/to/tv/dir:/tv -v /path/to/download/dir:/downloads linuxserver/sonarr
```

Now run
```
docker start sonarr
```

Browse to http://yourIP:8989 and you should see Sonarr. Sonarr will need to be configured to use Jackett but this is simple. Once that has been done TV shows can now be added. Sonarr will search for them via Jackett, import the torrent into RuTorrent and then post process once the download has finished.

## Post Installation
Now you can use something like Kodi to scan the TV directory and have all the TV shows all in one place. Kodi on a Raspberry Pi is a great combo for this type of automation.

Consider setting up reverse proxies for each of the services with a domain or sub-domain to help with easy access. Remembering IP addresses and port numbers is hard so make life easy with a reverse proxy. You can refer back to one of my [previous posts](/docker-nginx-and-lets-encrypt/) about setting up Ghost with a reverse proxy, the config for Sonarr, RuTorrent and Jackett will be extremely similar.

