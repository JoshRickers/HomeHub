+++
author = "Josh Rickers"
categories = ["Server"]
date = 2020-04-07T12:31:16Z
description = ""
draft = false
slug = "server-build-spec"
tags = ["Server"]
title = "Server Build Spec"

+++


I have been planning for a long time to build a server that is capable of running multiple Docker containers, Plex transcoding and a few Virtual Machines. For the past couple of years I have had a local Xpenology server that runs a version of Synology DSM without the need for Synology hardware. The hardware running this is quite old. DDR2 RAM and a motherboard that only has 2 SATA ports.

I was also running a Raspberry Pi for Home Assistant and Pi Hole. This was an ok solution but I wanted something with a bit more power to run multiple Docker containers. I was planning on running Docker on the Xpenology box but this required an update of the DSM software. While in the past upgrading DSM versions has been quite simple, upgrading to the version that I needed to get Docker running how I wanted was a bit more difficult. I was unable to find a network driver that was compatible with my motherboard. Because of this I ended up running a remote server for my Docker containers.

The remote server was hosted by OVH. It was one of their Kimsufi deals. i3, 8GB RAM and 2TB HDD which was more than enough power to run the Docker containers and also be my media server. This combination has been running fine for a few years now but I wanted a bit more oomph and to also have the possibility of playing 4K content when I eventually get round to buying a 4k TV.

---

## The Build

The build needs to be lowish budget and capable of running multiple VMs and docker containers. It also needs to be a smallish form factor. So, first thing would be to decide what case to use. I have looked into purchasing an actual rack mount server but the prices, size, power consumption and noise of  rack mount servers is something that I don't want to consider.

I currently own an Fractal Design S and this has been a superb case so Fractal Design was the first manufacturer that I checked out. Their main small NAS cases  seem to be the Node 304 and 804. The 304 doesn't house the size motherboard I want to use and would have limited space for the amount of storage I want to end up using. In the end I went with the 804 as this can house the motherboard I want to to use and also has plenty of space for storage. I looked into other cases, even tower cases but these defeated the small requirement.

Next up was CPU. I have been using Intel CPU's for the past decade or so and I haven't really been paying attention to the CPU market so my instinct was to look for a low cost i5. This was until I kept seeing deals popping up on Amazon for AMD Ryzen CPUs. Looking into these they are loaded with cores and threads of which many are needed for a running VMs and Docker containers. The Ryzen 2700x it the sweet spot of cost vs performance. 3.7GHz base clock, 8 cores and 16 threads.

Now I needed a motherboard that would fit my case and CPU choice. The Fractal Design Node 804 can handle a micro ATX motherboard which narrowed down my choices significantly. Checking out [PCPartPicker](https://pcpartpicker.com/) I found the MSI B450M Mortar Max. This can handle the Ryzen 2700x out of the box without the need of a bios upgrade and also DDR4 RAM, plenty of SATA ports to start with, M.2 and PCI slots.

RAM, DDR4. Amazon popped an offer that seemed to good to resist. 2 x 8GB Crucial Ballistix for £48.99. Down from £84.95. This should be plenty for the beginning and easily upgraded in the future when needed.

Next up is power supply. I had to purchase a new one for the Xpenology box a couple years a go so this I what I have been planning on using. Also keeps the cost down.

A Server needs storage. I have plenty of spare HDD lying around that I am going to repurpose. A couple from the Xpenology server and a couple from my gaming rig. Total space will be 4.5TB if everything goes well.

---

## Part List

* Case: Fractal Design Node 804
* CPU: Ryzen 2700x 3.7GHz 8c/16t
* Motherboard: MSI B450M Mortar Max mATX
* RAM: 16GB Crucial Ballistix Sport LT
* PSU: Corsair VS350
* Storage: Various HDDs

I am expecting the PSU and HDDs to  let me down. But as this is a "budget" build I wont be looking to upgrade them until I have to.

Next up. Building!

