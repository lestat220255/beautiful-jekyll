---
layout:     post
title:      "docker搭建gitlab和svn服务"
subtitle:   "实现免费的私有仓库"
date:       2018-05-21 17:15:59
author:     "Lestat"
header-img: "img/post-bg-2015.jpg"
catalog: true
bigimg:
    - /img/post-bg-2015.jpg
    - /img/post-bg-2018.jpg
    - /img/grizzly.adapt.1190.1.jpg
    - /img/home-bg.jpg
tags:
    - docker
    - gitlab
    - svn
toc: true
---

- [使用daocloud给docker加个速先...](#%E4%BD%BF%E7%94%A8daocloud%E7%BB%99docker%E5%8A%A0%E4%B8%AA%E9%80%9F%E5%85%88)
- [gitlab安装](#gitlab%E5%AE%89%E8%A3%85)
- [svn安装](#svn%E5%AE%89%E8%A3%85)
- [关于gitlab的系统资源占用](#%E5%85%B3%E4%BA%8Egitlab%E7%9A%84%E7%B3%BB%E7%BB%9F%E8%B5%84%E6%BA%90%E5%8D%A0%E7%94%A8)
- [总结](#%E6%80%BB%E7%BB%93)

> 之前公司里的代码都是托管到局域网服务器上的,现在由于部分同事远程办公的需要,计划把git和svn都转到公网的centos服务器上去,但是gitlab的配置是真心费时间,所以决定用docker来做这个事情,以下是一些步骤和总结  

### 使用daocloud给docker加个速先...
可以通过这个[链接](http://www.daocloud.io/mirror#accelerator-doc)里面的命令给docker改个源,不然速度慢死...

### gitlab安装  
1. 拉取镜像
```bash
docker pull gitlab/gitlab-ce:latest
```

2. 新建授权用户
```bash
useradd -d /home/gitlab -s /bin/sh -m gitlab
```

3. 后台运行容器,指定域名,端口映射关系,目录映射关系,将容器命名为gitlab,方便后续操作
```bash
docker run --detach \
  --hostname git.vcs.trycheers.com \
  --publish 10443:443 --publish 10080:80 --publish 10022:22 \
  --name gitlab \
  --restart always \
  --volume /home/gitlab/config:/etc/gitlab \
  --volume /home/gitlab/logs:/var/log/gitlab \
  --volume /home/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
```

1. 用apache对`10080`端口进行反代,使之能够通过域名访问  
```
<VirtualHost *:80>
 ServerName hostname
 ProxyPreserveHost On 
 ProxyPass / http://localhost:10080/
 ProxyPassReverse / http://localhost:10080/
</VirtualHost>
```

### svn安装  
1. 后台运行容器,指定端口映射关系,目录映射关系,将容器命名为svn,方便后续操作
```bash
docker run -d -p 9200:80 -p 9201:443 -v /home/subversion/svn:/var/local/svn -v /home/subversion/svn_backup:/var/svn-backup -v /home/subversion/svn_conf/:/etc/apache2/dav_svn/ --name svn marvambass/subversion
```

2. 添加svn用户  
```bash
htdigest /home/subversion/svn_conf/dav_svn.passwd Subversion username
```

3. 修改仓库/分组/用户权限
直接编辑`/home/subversion/svn_conf/dav_svn.authz`

1. 用apache对`9200`端口进行反代,使之能够通过域名访问  
```
<VirtualHost *:80>
 ServerName hostname
 ProxyPreserveHost On 
 ProxyPass / http://localhost:9200/
 ProxyPassReverse / http://localhost:9200/
</VirtualHost>
```

### 关于gitlab的系统资源占用  
看图说话
![](https://lestat.b0.upaiyun.com/blog/gitlab-stats.png)
在docker中常驻内存大概是2GB+,cpu开销通常只是在启动时候特别大,因此要运行`gitlab`推荐**至少**使用2核4GB的服务器配置!
> 哎,也难怪当时折腾半天也没能在我家树莓派(arm架构的4核cpu,512M内存...)上搞定`gitlab`...

### 总结
gitlab在刚启动时会加载大量的环境依赖,因此可能出现cpu占用高的情况,根据服务器性能不同会持续一段时间,通常在cpu占用降至正常时才能访问到本地的gitlab项目  
