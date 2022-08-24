+++
author = "Josh Rickers"
categories = ["Emby", "Kodi"]
date = 2019-01-23T11:31:34Z
description = ""
draft = false
slug = "installing-emby-for-kodi"
tags = ["Emby", "Kodi"]
title = "Installing Emby for Kodi"

+++


Kodi is a wonderful media client and I have been using it for many years now. I have been adding more clients to my home recently and have noticed some slight annoyances. The main one is the lack of synchronisation between Kodi clients. This can be solved with a MySQL server keeping track of everything but I don't have anything running locally to do this. Emby and the Kodi addon Emby for Kodi has fixed the synchronisation annoyance.

Emby is a media server that will store meta data, stream, transcode and synchronise all of your media in one place. I have this running on the server that stores all of my media. It is running on a Docker container which, in my opinion, is the easiest way. See [this blog post](/emby-media-server-with-docker/) on how to install Emby using Docker.

Emby for Kodi is an addon that will sync your Emby server with your Kodi client.

## Installing Emby for Kodi

This install works best on a fresh install of Kodi. At the time of writing this the current version of Kodi is 17.6.

Settings > File Manager > Add source. Type http://kodi.emby.media and give the media source a name. Click OK.

{{< figure src="/images/2019/01/image-4.png" >}}

Now browse to Add-ons, click the box icon in the top left corner and click Install from Zip file. If this is a fresh install you will get asked to allow unknown sources.

{{< figure src="/images/2019/01/image-5.png" >}}

{{< figure src="/images/2019/01/image-6.png" >}}

Click settings and then toggle Unknown sources. Press yes and go back to the Install from zip menu.

{{< figure src="/images/2019/01/image-7.png" >}}

Click on http://kodi.emby.media source you added earlier. Then click on repository.emby.kodi-x.x.x.zip.

{{< figure src="/images/2019/01/image-8.png" >}}

Now click on install from repository > Kodi Emby Addons > Video Addons > Emby. Then click Install.

{{< figure src="/images/2019/01/image-9.png" >}}

Once the install is complete you will get asked to sign in to your Emby server. You can do this using Emby Connect or by manually adding the server. Once added you will be asked to log in to an account if you have a password set up on the Emby server. You will then be asked to choose which play back mode you would like to use. I suggest using the default Addon option.

{{< figure src="/images/2019/01/image-10.png" >}}

It will ask you if you want to disable the Emby music library. This is up to you and whether or not you have music on your Emby server.

Browse back to Movies and TV and you should have all the media synced directly to your Kodi client.

{{< figure src="/images/2019/01/image-11.png" >}}

