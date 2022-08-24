+++
author = "Josh Rickers"
categories = ["Docker", "Ghost"]
date = 2018-05-31T17:34:55Z
description = ""
draft = false
slug = "installing-ghost-on-docker-in-2018"
tags = ["Docker", "Ghost"]
title = "Installing Ghost on Docker in 2018"

+++


I have been looking for a way to get a blog up and running in quick and simple manner. No installing and configuring databases. No installing and configuring web servers. Minimal user interaction when installing and setting up.

This is where Docker comes in to play.

## Docker
Minimal user interaction and you are using docker? yes i am.
Using Docker will only require me to install Docker and use ```docker run ...``` to get an instance of a working blog up and running, usually in seconds.

## #Installing Docker on Ubuntu 16.04
Run the following commands to install Docker.
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
```
sudo apt-get update
```
```
apt-cache policy docker-ce
```
```
sudo apt-get install -y docker-ce
```

## Installing Ghost
Ghost run an [official repository](https://hub.docker.com/r/library/ghost/) on the Docker Hub. This is where you can find the latest information regarding the official Ghost docker container.

As of 31st March 2018 the latest version of Ghost is 1.23.0 which is what we will be running. The following command will finally get Ghost up and running.

```
docker run --name nameofcontainer -p 3001:2368 -e url=yourdomain -v /path/to/home/folder/ghost/content:/var/lib/ghost/content --restart=always -d ghost:1.23.0-alpine
```

Make sure you replace the relevant arguments to suit you and that you use the most current version of ghost which can be found on their [repository](https://hub.docker.com/r/library/ghost/).

Now you can visit your IP:3001. 

The next task will be to configure a domain, reverse proxy and an SSL certificate. You can use Docker to run Nginx and Letsencrypt which will automate your SSL renewals. I will be posting about this soon!

