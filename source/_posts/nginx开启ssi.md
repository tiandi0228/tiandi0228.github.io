---
title: nginx开启ssi
date: 2016-09-06 20:44:16
tags:
- nginx
- ssi
---

### 进入nginx安装文件的目录
```
cd /root/nginx-1.11.3/src/http/modules
```

### 编辑如下文件
```
vi ngx_http_ssi_filter_module.c
```

### 注释以下（大约 2065 到2067）行，或者搜索 ngx_http_parse_unsafe_uri 找到如下代码：
```
2065 // if (ngx_http_parse_unsafe_uri(r, uri, &args, &flags) != NGX_OK) {
2066 //    return NGX_HTTP_SSI_ERROR;
2067 // }
```

### 保存以上文件
```
cd /root/nginx-1.11.3
执行./configure --prefix=/usr/local/nginx --with-poll_module --with-http_stub_status_module
执行 make （注意，此处只需要执行make ，不需要 执行make install）
```

### 备份nginx 安装目录下的nginx 文件，执行如下脚本
```
进入目录：cd /usr/local/nginx/sbin/
停止nginx ：./nginx -s stop
执行： mv nginx /home/nginxold
```

### 将刚才第5步编译好的nginx文件从（/root/nginx-1.11.3/objs）拷贝到/usr/local/nginx/sbin/ 目录下
```
进入objs目录 cd /root/nginx-1.11.3/objs
拷贝nginx文件：cp nginx /usr/local/nginx/sbin/nginx
```

### 启动nginx
```
进入cd /usr/local/nginx/sbin/ 目录
启动：./nginx
```