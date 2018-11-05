---
title: vue-route刷新页面出现404
date: 2016-12-20 20:48:13
tags: 
- vue 
- 404
---

把做好的Vue一个小网站build到服务器上刷新了一下页面出现404错误，然后通过百度找了问题。

```
location / {
    try_files $uri $uri/ @router;
    index index.html;
}
location @router {
    rewrite ^.*$ /index.html last;
}
```