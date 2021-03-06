---
layout:     post
title:      "关于docker内nginx获取真实client-ip的问题"
subtitle:   "MacOS有坑"
date:       2018-11-09 22:55:00
author:     "Lester"
bigimg:
    - /img/post-bg-2015.jpg
    - /img/post-bg-2018.jpg
    - /img/grizzly.adapt.1190.1.jpg
    - /img/home-bg.jpg
catalog: true
tags:
    - docker
    - nginx
toc: true
---

- [环境](#%E7%8E%AF%E5%A2%83)
- [问题](#%E9%97%AE%E9%A2%98)
- [原因](#%E5%8E%9F%E5%9B%A0)
- [方法](#%E6%96%B9%E6%B3%95)
- [现存问题](#%E7%8E%B0%E5%AD%98%E9%97%AE%E9%A2%98)

### 环境
系统:MacOS Mojave  
web环境:docker+nginx+php-fpm

### 问题
nginx始终无法获取到正确的客户端ip地址,获取到的是nginx所在docker容器的网关ip

### 原因
后来发现是MacOS下才有的问题,在linux下正常

### 方法
在nginx配置文件的`server`段加入以下
```
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header Host $http_host;
proxy_set_header X-NginX-Proxy true;
```

### 现存问题
当前配置可在linux下获取到正确的客户端ip,但macOS系统获取到的依然是gateway地址,目前多次google后仍然无果,以下为部分该问题相关的参考地址  
[Original ip is not passed to containers](https://github.com/docker/for-mac/issues/180)  
[Docker Beta on Mac : Cannot use ip to access nginx container](https://stackoverflow.com/questions/38340110/docker-beta-on-mac-cannot-use-ip-to-access-nginx-container)  
[docker 如何让 Nginx 获取到访问者 IP?](https://www.v2ex.com/t/488997)  

> 后续需要继续关注该问题的解决方案
