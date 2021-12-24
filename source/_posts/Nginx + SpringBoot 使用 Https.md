---
title: Nginx + SpringBoot 使用 Https
date: 2018-07-31 20:51:19
tags: 
- nginx 
- SpringBoot 
- https
---

```
http {
# Tomcat 服务器集群
upstream stock {
        server 127.0.0.1:8080 weight=4;
        server 127.0.0.1:8081 weight=2;
        server 127.0.0.1:8082 weight=1;
}

server {
        listen  443 ssl;
        listen  [::]:443 ssl;
        server_name 绑定的域名;
        ssl on;     
        ssl_certificate  证书.pem;
        ssl_certificate_key  证书.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        location / {
            proxy_redirect   off;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            # 把 https 的协议告知 Tomcat，否则 Tomcat 可能认为是 http 的请求
            proxy_set_header X-Forwarded-Proto $scheme;
            # 请求转发给 Tomcat 集群处理
            proxy_pass http://stock;
        }
    }
}
```
