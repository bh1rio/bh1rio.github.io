---
layout: post
title: 当时用Docker运行GitLab时的非80端口HTTP服务
date: 2017-11-28 08:29:25
categories: Docker Git
tags: Docker Git
---

我不知道多少人会像我一样在家里使用Docker来跑GitLab，如果真有，那么一定会与到和我一样的问题。我遇到的问题比较简单：宽带运营商不开放80端口，GitLab的Docker镜像默认只支持80端口。外网端口直接端口映射可以用，但是在gitlab的网站里面看到git的clone路径的端口是有问题的，或者地址也是内网的。

解决这个问题需要预先确定准备使用什么域名和端口。首先需要一个动态域名，老tp-link路由器可以使用花生壳，新的tp-link路由器可以用tp-link提供的动态域名，比如现在有一个叫 xx456.tpddns.cn的域名。然后需要确定使用什么端口，比如我映射在2080上。那么我们可以用如下的命令创建一个Docker容器：

```bash  
docker run \
-e GITLAB_OMNIBUS_CONFIG="external_url 'http://xx456.tpddns.cn:2080’;” \
–p 22:22 –p 2080:2080 \
--name gitlab \
--restart always \
-v /srv/docker/gitlab/config:/etc/gitlab \
-v /srv/docker/gitlab/logs:/var/log/gitlab \
-v /srv/docker/gitlab/data:/var/opt/gitlab \
-d gitlab/gitlab-ce:latest
```

其中

* 如果你不准备使用ssh访问gitlab里面的git的话，那个22端口的映射也可以去掉。
* 环境变量GITLAB_MNIBUS_CONFIG里面的external_url就是gitlab提示的地址，gitlab会自动判断是使用http还是使用https，自动判断是使用默认端口，还是其中配置的接口。

现在LAN用ip访问一下，然后再在路由器上做外网2080端口到docker所在服务器192.168.1.2的2080端口的映射。这样无论以后在外网还是内网，都可以使用<http://xx456.tpddns.cn:2080>来访问这个docker容器中的gitlab了。

注意：不知道什么原因，这种方式做的gitlab容器，会比默认情况下创建的gitlab启动的要慢，也就是docker容器重启以后，由starting到health状态花费的时间要多，初步估计会多30%到50%，但是运行起来之后没有区别。

> 2025-08-28 注: gitlab太占内存了，跑起来需要1G的内存。还是gitea香。