+++
author = "Josh Rickers"
categories = ["Docker", "Ghost", "Nginx", "Let's Encrypt"]
date = 2018-06-02T19:41:23Z
description = ""
draft = false
slug = "docker-nginx-and-lets-encrypt"
tags = ["Docker", "Ghost", "Nginx", "Let's Encrypt"]
title = "Docker, Nginx and Let's Encrypt"

+++


In my previous blog post I explained how quick and easy it was to get a Ghost blog up and running using docker. The next step is to set up a reverse proxy and an SSL certificate. I will be using Nginx as the reverse proxy and Let's Encrypt as my SSL certificate provider. All with the help of Docker!

## The Container
There are many Docker containers available, some official and others provided by the community. In my search for a well maintained container I came across [linuxserver.io](https://www.linuxserver.io/). They provide a vast amount of containers readily available and easy to use. The container we will be using is their [Let's Encrypt container](https://hub.docker.com/r/linuxserver/letsencrypt/) which also contains Nginx, how helpful!

You will need to run the following command to set everything set up.

```
docker create --cap-add=NET_ADMIN --name=letsencrypt -v /path/to/home/letsencrypt:/config -e PGID=1000 -e PUID=1000  -e EMAIL=youremail -e URL=yoururl -e SUBDOMAINS=any,subdomains -e EXTRA_DOMAINS=extradomains -p 443:443 -p 80:80 -e TZ=Europe/London -e HTTPVAL=true linuxserver/letsencrypt
```

Fill in the command with your information and omit anything you do not require, like extra domains and sub-domains. PGID and PUID are the group and user ID for my user. If you do not know these and have not configured Docker to run without sudo then just sudo the command.

The next thing to do is to run the container
```
docker start letsencrypt
```

## The Reverse Proxy
Now that you have the container set up and running we will need to configure the Nginx config to run the reverse proxy. Using my Ghost setup as an example.

```
nano /path/to/letsencrypt/nginx/site-confs/default
```

You will now the see the default config for Nginx. Copy and paste in the following at the end of the document.

```
server {
       listen 443 ssl;

       root /config/www;
       index index.html index.htm index.php;

       server_name yourdomainnames;

       ssl_certificate /config/keys/letsencrypt/fullchain.pem;
       ssl_certificate_key /config/keys/letsencrypt/privkey.pem;
       ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE--RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
       ssl_dhparam /config/nginx/dhparams.pem;
       ssl_prefer_server_ciphers on;

       client_max_body_size 0;

       location / {
               include /config/nginx/proxy.conf;
               proxy_pass http://youripaddress:3001;
       }
}
```

Make sure to replace the domain names and the IP address with your domains names and IP address.

Restart the Docker container, wait a few seconds and try your domain in your web browser. If everything was successful you should see your Ghost blog!

