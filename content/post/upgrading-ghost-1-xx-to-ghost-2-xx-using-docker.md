+++
author = "Josh Rickers"
categories = ["Ghost", "Docker", "Install"]
date = 2019-01-19T19:55:04Z
description = ""
draft = false
slug = "upgrading-ghost-1-xx-to-ghost-2-xx-using-docker"
tags = ["Ghost", "Docker", "Install"]
title = "Upgrading Ghost 1.xx to Ghost 2.xx using Docker"

+++


Checking my Ghost installation recently and I noticed i was way out of date and needed to updated to the latest version of Ghost ( currently 2.11.1 ). Now usually this would have been the case of simply following the upgrade instructions provided by Ghost but because I am running Docker the upgrade process was slightly different.

---

Before upgrading to 2.xx you will have to be on version 1.25.6 as this has the latest database changes that are compatible with the latest version.

And before any of these commands make sure you have backed up your Ghost blog by downloading the JSON file from the admin control panel >  Labs > Export your content.

You will need to stop and remove the current running Docker container. dockercontainer being the name you used for your container

```
docker stop dockercontainer
docker rm dockercontainer
```

Now you want to run the Ghost image for 1.25.6. I chose to run the Alpine version.

```
docker run --name dockercontainer -p 3001:2368 -e url=https://yoururl.com -v /path/to/ghost/content:/var/lib/ghost/content --restart=always -d ghost:1-alpine
```

Now go and check your Ghost blog to make sure everything is functioning correctly. If so we now can jump Ghost 2!

Again, stop and remove the current container.

```
docker stop dockercontainer
docker rm dockercontainer
```

Now pull and run Ghost 2. Make sure to keep the path to your Ghost content the same.

```
docker run --name dockercontainer -p 3001:2368 -e url=https://yoururl.com -v /path/to/ghost/content:/var/lib/ghost/content --restart=always -d ghost:2-alpine
```

Check your Ghost blog, it can take a minute or two to come back online but everything should be up and running.

