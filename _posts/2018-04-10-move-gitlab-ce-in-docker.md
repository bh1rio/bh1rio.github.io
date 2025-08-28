---
layout: post
title: 迁移docker方式安装的gitlab-ce
date: 2018-04-10 10:55:40
categories: Docker Git
tags: Docker Git
---

之前用Docker的方式在阿里云给公司部署了1台Gitlab CE，当时觉得部署起来很简单方便。这次公司要把这个git迁移会IDC，记录过程如下：

1. 暂停老服务器的服务

```bash
docker stop gitlab
```

2. 迁移数据

  进入新服务器的`/srv`目录，sftp到老服务器，执行`get –r /srv/gitlab /srv`

  -r参数会把整个目录都拿下来

3. 新服务器启用安装docker

  略

4. 下载gitlab-ce镜像

  略

5. 运行容器

  按照 https://docs.gitlab.com/omnibus/docker/ 中 Run the Image章节运行。

6. 迁移预处理

```bash
docker exec -it gitlab update-permissions
docker restart gitlab
```

再重启之后，重新对域名做解析，gitlab服务就正常了。

另，gitlab文档说更换image的版本，可以实现升级，有闲的兄弟可以试试，哈哈
