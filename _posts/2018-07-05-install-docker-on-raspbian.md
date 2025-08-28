---
layout: post
title: Raspbian上安装Docker
date: 2018-07-05 14:24:10
categories: Docker RaspberryPi
tags: Raspbian
---

习惯了Arch的仓库以后，Raspbian的仓库老的不能再老了。查了Docker的网站，不能直接装，需要用如下的方法，先搞下来一个脚本来安装，速度有点慢：

```bash
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

真的是有慢，用的docker官方的仓库。

> 2025-08-28 注: docker.com被墙了，但是可以使用国内的docker网站镜像安装。比如tuna。

