---
layout: post
title: 用yum给centos7安装nginx
date: 2017-08-21 03:27:30
categories: Linux
tags: Linux nginx
---

最近使用阿里云上的centos7的时候，发现直接yum install的nginx版本比较低，鉴于我是新版本强迫症，研究了一下怎么用nginx预编译的包，而不是centos仓库自带的。如下

1. 在/etc/yum.repos.d目录下创建nginx.repo文件，内容如下：

```ini
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

2. 再用yum install nginx的时候，可以看到已经是最新的版本了。

这样做的好处有几个，可以直接用systemctl来控制Nginx服务了，再有以后yum update也能跟着更新。
