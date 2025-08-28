---
layout: post
title: CentOS安装Docker-CE
date: 2017-12-05 10:38:53
categories: Docker Linux
tags: centos Docker
---

原本CentOS7里面的Docker是1.12版本的，没觉得很老，但是在自动化构建asp.net core的时候，不支持Dockerfile中的FROM AS语法，只好查一下CentOS7下怎么安装新的Docker-CE，如下：

```bash
yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce
systemctl start docker
```

目前安装的是17.09.0-ce版本

> 2025-08-28 注: centos没了，docker也访问不了。唉