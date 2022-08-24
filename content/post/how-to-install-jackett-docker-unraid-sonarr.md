+++
author = "Josh Rickers"
categories = ["Docker", "Automation", "Install", "Jackett", "Sonarr", "Unraid"]
date = 2020-08-22T19:53:51Z
description = ""
draft = false
slug = "how-to-install-jackett-docker-unraid-sonarr"
tags = ["Docker", "Automation", "Install", "Jackett", "Sonarr", "Unraid"]
title = "How to install Jackett and connect with Sonarr on Unraid using Docker"

+++


My previous post set you up with installing Sonarr on Unraid but that was as far as we got. In this post I want to show you how to set up Jackett and connect to Sonarr so you can connect to torrent trackers that are not oficially suported by Sonarr. This also works for Radarr and has an extremely similar set.

First thing first, lets install the Jackett Docker container. As always I will be using Linuxserver.io containers. You will need to browse to your the Apps tab and then search for Jackett, click on the icon for the containter you want and then click install.

{{< figure src="/images/2020/08/image.png" >}}

Now for the settings. You want to have something similar to the settings in the screenshot below.Name: The name you want to call the containerRepository: The repository (probably wont need to change this)Network Type: You can leave this as defaultHost Port 1: This is the port user for the container. Make sure this is unique.Host Path 2: This needs to be the full path to your downloads folder. I am using the rutorrent container and the file path I have set here is the download folder set in the rutorrent container. Key 1: This can be left as default unless you have changed the PUIDKey 2: This can be ledt as default unless you have changed the PGID

{{< figure src="/images/2020/08/image-1.png" >}}

Then click apply. This will then download and install the docker container.

Once this is installed you can then click on the image icon and then click WebUI. This will open the Jackett web interface. Once the interface as load you need to make a note of the api key in the top right corner. Open Sonarr and then go to settings > Indexers. Click the big plus sign and select Torznab. For the URL you need to go back to the jackket and click on Copy Torznab Feed button. Past this into the URL box.In the API Key box, copy and paste the API Key we made a note of earlier from Jackett. You can then select the Categories used by the torrent tracker. Click test to make sure it all links up and then click save.

{{< figure src="/images/2020/08/image-3.png" >}}

Back into Jackett and we can click Add Indexer. Scroll through /  search for the site you use and click the configure button (spanner icon). From here you can see a list of categories and also fields for log in credentials. Fill these out and click OK.

You will now be able to search for TV shows in Sonarr using torrent trackers.

