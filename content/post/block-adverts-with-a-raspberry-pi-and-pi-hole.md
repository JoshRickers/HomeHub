+++
author = "Josh Rickers"
categories = ["Raspberry Pi"]
date = 2018-06-21T09:19:51Z
description = ""
draft = false
slug = "block-adverts-with-a-raspberry-pi-and-pi-hole"
tags = ["Raspberry Pi"]
title = "Block Adverts with a Raspberry Pi and Pi-hole"

+++


You can use a Raspberry Pi and some wonderful open source software called Pi-hole to block adverts on your entire home network!

<iframe width="560" height="315" src="https://www.youtube.com/embed/h-bfQWc9GGQ" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

I have a couple Raspberry Pis, an old model 1 and a newer model 3. The model 3 is being used to run Home Assistant (home automation software) and the other was being used to run Kodi but I now have a Steam Link which I mainly use for Kodi so the Raspberry Pi was gathering dust.

Blocking adverts on PC is easy, slightly more difficult on mobile devices. Then I discovered Pi-hole which will block adverts on any device connected to the same network.

## Raspbian
First thing we need to do is install an OS that we can use to run Pi-hole. I suggest using Raspbian as it is easily available you can download this straight from the Raspberry Pi website.
We will be using the Lite version for this as we do not need to run a full desktop environment.

Skip this step if you already have a Raspberry Pi running on OS.

Browse to https://www.raspberrypi.org/downloads/raspbian/ and download the RASPBIAN STRETCH LITE file.

Next we need to flash this to your SD card. It is suggested that we use a program called Etcher. So visit https://etcher.io/ and download and install this if you don't already have it.

Etcher is pretty straight forward to use with only 3 steps to follow:
1. Select your image (the Raspbian Stretch Lite we downloaded earlier)
2. Select your SD card
3. Flash!

This can take some time. Once it has finished there is one more step before we can plug this in and boot up the Raspberry Pi.

## Enable SSH
SSH is disabled by default when using Rasbian so we need to enable this as we will not be plugging this into a monitor. 
Browse to the root of the SD card you have just flashed and create a blank file called SSH. The easiest way to do this is right click > New > Text Document. Rename this file to SSH, all capitals and remove any file extensions.

Now plug the SD card into your RPI, connect the power and a network cable and wait a few minutes for it to boot.

## Pi-hole
You can find the IP address of your RPI by looking at the DHCP table on your router. Once you have found this you will need to SSH to it. You can use Putty or any other SSH client.

The default username is pi and the default password is raspberry.

Next we are going to run the install command that can be found on https://pi-hole.net/ 

```
curl -sSL https://install.pi-hole.net | bash
```

This will run through the installer. This has minimal interaction and only requires the user to select their forwarding DNS servers (Google, OpenDNS, Cloudflare etc...) and enabling the admin console and logging. Another easy straight forward install.

The last step is to configure your devices to be use Pi-hole as their DNS servers. This is simple enough to do per device and some routers allow you to configure what DNS servers to use. If you have a router that does not allow this then Pi-hole can be configured to be the DHCP of the network allowing any device to receive the correct network settings.

