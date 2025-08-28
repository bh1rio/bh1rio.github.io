---
layout: post
title: 开启Docker的远程管理功能
date: 2017-11-09 07:38:47
categories: Docker
tags: 
---

摘录自 https://docs.docker.com/engine/admin/#configure-the-docker-daemon

首先修改`/etc/docker/daemon.json`文件，添加：

```json
"hosts": ["unix:///var/run/docker.sock","tcp://192.168.59.3:2376"]
```

如果这个文件不存在，就创建一个。如果存在，注意这个文件是json格式，添加新的行，注意上一行末尾添加逗号。

然后再用`systemctl show --property=FragmentPath` docker找到服务的定义文件，然后去掉ExecStart那一行的-H参数，修改为：

```
ExecStart=/usr/bin/dockerd
```

这样重启整个系统就好了。不愿意重启的话，先`systemctl daemon-reload`，再`systemctl restart docker`。

> 2025-08-28 注: daemon-load使服务定义文件重新加载，单纯修改deamon.json的话，不需要这句，直接restart就好。
