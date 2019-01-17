---
layout:     post
title:      "php开启opcache前后性能差异"
subtitle:   "php-fpm性能优化"
date:       2019-01-17 15:19:00
author:     "Lestat"
bigimg:
    - /img/post-bg-2015.jpg
    - /img/post-bg-2018.jpg
    - /img/grizzly.adapt.1190.1.jpg
    - /img/home-bg.jpg
catalog: true
tags:
    - docker
    - opcache
---

**本打算发帖到v2ex上求助,结果自己碰巧解决了,因此在博客上记录一下完整的从发现到解决的过程**   

### 环境
硬件配置:腾讯云的2核4G服务器  
系统:ubuntu server 16.04 LTS  
lnmp:通过docker-compose做编排的php-fpm7.2(基于alpine)+nginx(官方镜像)+mysql5.7(官方镜像)  
缓存:redis  
框架:laravel5.5  

### 之前QPS
* 不改变入口文件,请求`http://hostname/`,**QPS:19-21**
* 不改变入口文件,请求`http://hostname/任意路径`,**QPS:18-19**
* 在入口文件第二行直接`die();`,请求`http://hostname/`,**QPS:240-250**

### 已做过的调试
1. 开启了php-fpm的slowlog记录(并确保其正常工作:docker开启了cap_add: SYS_PTRACE),但通过压测工具并未发现slowlog有任何记录(代码里加`sleep(2)`会记录到slowlog里)
2. 已经用过laravel自带的配置缓存,路由缓存以及optimize等命令
3. 已开启opcache

### 其他说明
服务器通过nginx监听80端口对来源请求进行反向代理至php所在容器进行处理,所有容器中只有nginx对外开放了80和443,其他都是容器内部通过`container_name`进行访问

### 问题
可以从哪些方面着手提高QPS?


### 问题解决-开启opcache
[opcaches是什么](http://php.net/manual/zh/intro.opcache.php)  
**以下是开启opcache和关闭后QPS的对比**  
```bash
#开启opcache（Dockerfile中使用docker-php-ext-install opcache）
➜  ~ http_load -p 80 -s 30 url
2201 fetches, 80 max parallel, 1.33667e+07 bytes, in 30 seconds
6073 mean bytes/connection
73.3667 fetches/sec, 445556 bytes/sec
msecs/connect: 4.99642 mean, 32.34 max, 2.791 min
msecs/first-response: 1066.44 mean, 2130.71 max, 52.395 min
HTTP response codes:
  code 200 -- 2201
➜  ~ http_load -p 80 -s 30 url
2389 fetches, 80 max parallel, 1.45084e+07 bytes, in 30 seconds
6073 mean bytes/connection
79.6333 fetches/sec, 483613 bytes/sec
msecs/connect: 4.92044 mean, 41.46 max, 2.818 min
msecs/first-response: 980.024 mean, 1819.01 max, 42.171 min
HTTP response codes:
  code 200 -- 2389


#关闭opcache(未安装opcache)
➜  ~ http_load -p 80 -s 30 url
555 fetches, 80 max parallel, 3.37052e+06 bytes, in 30 seconds
6073 mean bytes/connection
18.5 fetches/sec, 112350 bytes/sec
msecs/connect: 5.68439 mean, 31.76 max, 2.826 min
msecs/first-response: 4035.69 mean, 5985 max, 120.81 min
HTTP response codes:
  code 200 -- 555
➜  ~ http_load -p 80 -s 30 url
559 fetches, 80 max parallel, 3.39481e+06 bytes, in 30 seconds
6073 mean bytes/connection
18.6333 fetches/sec, 113160 bytes/sec
msecs/connect: 5.78894 mean, 18.31 max, 2.944 min
msecs/first-response: 3970.26 mean, 5100.76 max, 163.014 min
HTTP response codes:
  code 200 -- 559
```

> 最后:通过打开`opcache`,QPS从20提升到了80.目前项目时间紧,抽不出时间来使用swoole进行解析,尝试过`laravels`这个开源胶水项目,但发现不少坑,遂暂时放弃,后续如果需要将单机性能提升到极致,仍然需要使用swoole代替php-fpm!