---
title: 隐藏 nignx php 隐藏
date: 2015-07-22 20:40:14
tags: 
- nignx 
- php
---

### 一、隐藏 Nginx 版本号
编辑 NGINX.CONF 文件，增加一行 SERVER_TOKENS OFF;

### 二、隐藏 PHP 版本号
编辑 PHP.INI 文件，在最后增加如下内容：
```
;;;;;;;;;;;;;;;;;
; Miscellaneous ;
;;;;;;;;;;;;;;;;;
; Decides whether PHP may expose the fact that it is installed on the server
; (e.g. by adding its signature to the Web server header).  It is no security
; threat in any way, but it makes it possible to determine whether you use PHP
; on your server or not.
; http://www.php.net/manual/en/ini.core.php#ini.expose-php
 expose_php = Off
```