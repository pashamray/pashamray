---
title: "ssh ports forwarding"
date: 2024-03-06T11:22:28+01:00
authors: ["pashamray"]
description: "ssh port forwarding"
tags: ["ssh", "ports", "forwarding"]
---
# Port forwarding

nginx config

```nginx
server {
  listen [::]:443 ssl;
  listen 443 ssl;

  server_name tun.site.xyz;

  location / {
    proxy_set_header Host $host;
    proxy_pass https://localhost:5443;
  }

  ssl_certificate /etc/letsencrypt/live/tun.site.xyz/fullchain.pem; # managed by Certbot
  ssl_certificate_key /etc/letsencrypt/live/tun.site.xyz/privkey.pem; # managed by Certbot
}

server {
  listen [::]:80;
  listen 80;
  
  server_name tun.site.xyz;
  
  location / {
    proxy_set_header Host $host;
    proxy_pass http://localhost:5080;
  }
}
```

```shell
ssh -f -N -R 5443:localhost:443 tun.site.xyz
```

### links

https://ngrok.com \
https://serveo.net
