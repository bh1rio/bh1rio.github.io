---
layout: post
title: 给docker中的mongodb开启权限
date: 2017-12-27 11:34:32
categories: Docker
tags: Docker MongoDB
---

先创建docker容器

```bash
docker run --name=mongodb -p 27017:27017 --restart=always -d mongo:3.6.0 --auth
```

在启动容器的bash

```bash
docker exec -it mongodb mongo admin
```

然后在提示符后执行

```
db.createUser({ user: 'admin', pwd: 'admin', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
```

说明：

1. 使用的是docker官方的镜像
2. 创建容器的时候，在最后要加—auth
3. 执行创建管理用户的以后，登录会需要选择用户的管理库为admin
4. 之后创建其他库的访问账号，也要在admin内创建账号，再分配其他库的权限。
