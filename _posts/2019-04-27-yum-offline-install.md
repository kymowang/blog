---
layout: post
title: 'yum离线安装'
date: '2019-04-27'
header-img: "img/home-bg.jpg"
tags:
     - yum
author: 'kymo'
---

# 离线安装yum包

CentOS服务器需要安装软件比如nginx, tomcat等，但是服务器大多不能连接内网，虽然有rpm包能用，但是rpm的依赖关系很难处理。

处理办法：

1. 在联网的机器上缓冲安装包

   ```
   vim /etc/yum.conf
   cachedir=/var/cache/yum/$basearch/$releasever
   # 原来的值是0
   keepcache=1
   ```

2. 安装需要的软件，比如nginx
   `yum -y install nginx`
3. 把缓冲的文件打包
   对于CentOS7，位置是`/var/cache/yum/x86_64/6/base/packages`
   ```tar -zxf /var/cache/yum/x86_64/6/base/packages```
4. 到服务器上把对应的文件恢复到原来位置，就可以用yum安装了

[参考：如何建立自己的离线yum源](https://blog.51cto.com/gforce/1367747)
