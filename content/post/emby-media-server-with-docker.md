+++
author = "Josh Rickers"
categories = ["Emby", "Docker"]
date = 2019-01-20T20:38:34Z
description = ""
draft = false
slug = "emby-media-server-with-docker"
tags = ["Emby", "Docker"]
title = "Emby Media Server with Docker"

+++


I have been looking into what would be the best solution for a media server. Currently all my media is on as server and I have kodi access this via FTP. Kodi deals with all the meta data, TV show information and Movie information. This works well but when you start to add more Kodi clients nothing stays in sync. You need to manually mark your watched items on the device you haven't watched them on or run up a MySQL server to keep track. Both of these options seem tedious and there must be a better solution.

Plex sprang to mind and I actually had this installed but when I went to access the server it asked me to register for a Plex account. This was something I did not want to do. I want to keep everything local and with no registration involved. I have also heard about some horror stories involving Plex and privacy.

This is where Emby comes into play. Someone I follow on twitter posted an article about switching from Plex to Emby and this gave me the motivation to give it ago myself.

Here are the simple steps to get your very own Emby media server up and running with Docker. If you haven't installed Docker already you can check out [this post](/installing-ghost-on-docker-in-2018/) It is slightly out of date now but the installation should be similar.

Create the config directory for Emby

```
mkdir -p emby/config/
```

Make note of your current locations for your media. This will be used to mount the volume in the Docker container.

```
docker create --name=emby --net=host --restart=always -e VERSION=latest -e UID=1000 -e GID=1000 -e TZ=Europe/London -v /path/to/emby/config:/config -v /path/to/tv:/mnt/tv -v /path/to/movies:/mnt/movies emby/embyserver:latest
```

The final thing to do now is run Emby.

```
docker run emby
```

Now visit http://yourip:8096 and follow the final install instructions. In the end you should have something like the following:

{{< figure src="/images/2019/01/image.png" >}}

From here you can start streaming your media straight from your browser and cast it to a chromecast device.

