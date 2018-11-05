---
title: 开启https
date: 2016-10-14 20:47:28
tags: 
- https
---

前几天购买了一个新域名（syc.im），然后在阿里云做解析的时候看到一个“18元一年云解析DNS热销版送CA证书”活动，就顺手购买了，折腾了几天终于把https服务开启来了^ v ^。

```
server {
    listen       443;
    listen       80;
    server_name  syc.im;

    if ($server_port = 80) {
        return 497;
    }

    #ssl
    ssl on;
    ssl_certificate /etc/nginx/conf.d/sslkey/213920636370985.pem;
    ssl_certificate_key /etc/nginx/conf.d/sslkey/213920636370985.key;
    ssl_session_timeout 5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers AESGCM:ALL:!DH:!EXPORT:!RC4:+HIGH:!MEDIUM:!LOW:!aNULL:!eNULL;
    ssl_prefer_server_ciphers on;
    error_page 497 https://$host$request_uri;
}
```