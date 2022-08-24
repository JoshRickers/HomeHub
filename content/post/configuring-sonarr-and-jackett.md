+++
author = "Josh Rickers"
categories = ["Sonarr", "Jackett", "Automation"]
date = 2018-06-14T20:13:47Z
description = ""
draft = false
slug = "configuring-sonarr-and-jackett"
tags = ["Sonarr", "Jackett", "Automation"]
title = "Configuring Sonarr and Jackett"

+++


In one of my previous [blog posts](/automate-tv-shows-with-sonarr/) I explained how to install Sonarr, Jackett and RuTorrent using Docker. This is a follow on post from that with some information on how to configure both Sonarr and Jackett. 

I thought this would need a little explaining as I left out some details from the previous post as I thought it is pretty self explanatory but you can never be too helpful. I know it would have helped me a lot if there was a nice blog post or two explaining a few details when i was looking into setting everything up. Hopefully this post will help anyone in the future!

## Sonarr
First thing you will see when opening Sonarr will be something similar to this:

![SonarrHomePage](/content/images/2018/06/SonarrHomePage.PNG)

You will want to click on settings on the menu bar to open the settings menu. This is where we will spend most of the time configuring Sonarr.

The first thing we want to do is add a download client. In this example I will be using rTorrent as this is what we have previously installed. 
Click Download Client > Big plus symbol. This will open a menu where you can select your download client from. Click rTorrent.

![DownloadClient](/content/images/2018/06/DownloadClient.PNG)

Now you will see a menu where you can fill out the connection details to your rTorrent session. Fill this menu out and click test. If everything is filled out correctly the test will succeed and you can click Save

![rTorrentSettings](/content/images/2018/06/rTorrentSettings.PNG)

## Jackett
On the homepage of Jackett there is a brief explanation on how to add Jackett as an Indexer to CouchPotato, Sonarr and Radarr. Very easy to follow but there is no explanation on how to set up indexers on Jackett.

To add an indexer you will need to click the green Add indexer button from the menu just under the API key ( you will need this later ).
A huge list of indexers will show find the one you use and click this spanner icon. This will open the settings menu for this indexer. You will have to fill out the information there and click save.

Repeat these steps for as many indexers as you use.

## Sonarr + Jackett
Now we need to configure Sonarr to use Jacket. Back on the Sonarr settings page click the Indexers tab and then the big plus symbol.

![IndexerMenu](/content/images/2018/06/IndexerMenu.PNG)

Click on Torznab > Custom.

![TorznabMenu](/content/images/2018/06/TorznabMenu.PNG)

Fill this out with the relevant information. Remember the API key from earlier, this is needed to authenticate Sonarr with Jackett. Once complete press save.

Everything should now be correctly set up and you can start adding TV shows to be scheduled in for download.

