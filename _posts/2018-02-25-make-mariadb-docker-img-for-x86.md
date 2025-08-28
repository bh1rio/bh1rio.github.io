---
layout: post
title: 给i686制作mariadb的docker镜像
date: 2018-02-25 09:29:32
categories: Docker Linux MySQL
tags: Docker Linux MySQL
---

不知道Docker公司是怎么想的，明明其Dockerfile没有指定必须x64，却不提供i686的镜像，只好每次有新版本的时候，重新制作一次。步骤如下：

1. 先从Docker公司的github里面获取最新的Dockerfile

```bash
git clone https://github.com/docker-library/mariadb.git
```

2. 进入mariadb/10.2目录，然后执行

```bash
docker build –t mariadb:10.2.13 .
```

然后等着就好了。

建议开始之前，先把debian:jessie升级到最新，这样能省很多debian做apt update的时间。
