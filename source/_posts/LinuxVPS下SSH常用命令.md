---
title: Linux VPS下SSH常用命令
date: 2012-09-11 19:46:55
tags: 
- SSH 
- Linux
---

```
rm -rf list #######删除list目录#######
zip –r list .zip ./* #######压缩zip文件#######
unzip list .zip #######解压zip文件#######
wget http://www.wisay.org/list.zip #######下载文件#######
/etc/init.d/nginx restart      ####### 伪静态重启#######
kill -QUIT 进程号 #######从容停止Nginx#######
kill -TERM 进程号 #######快速停止Nginx#######
pkill -9 nginx #######强制停止Nginx#######
service nginx start #######启动Nginx#######
service nginx stop #######停止Nginx#######
service nginx restart  #######重启Nginx#######
service mysql start #######启动mysql#######
service mysql stop  #######停止mysql#######
```