---
layout: post
title: 关于此次Archlinux的Base安装包组变化带来的影响
date: 2019-10-23 05:51:41
categories: Linux
tags: Archlinux
---

按照Archlinux的新闻稿，在2019年10月6日更新了Base安装包组，这里面只留下了必要的软件包，https://www.archlinux.org/news/base-group-replaced-by-mandatory-base-package-manual-intervention-required/

但是根据我的试验，不只其新闻稿中说的kernel、kernel-firmware和editor被移走，netctl、dhcpcd也被挪走了。而wiki的Install Guide却没有提及，这导致在安装完成后，实际是没有办法连接网络的，或者我不知道怎么连接网络了。经过试验需要把如下的安装根文件系统的语句

```bash
pacstrap /mnt base
```

替换为

```bash
pacstrap /mnt base linux linux-firmware netctl dhcpcd vi
```

其目的是补全base中移走的内容，保证安装完毕重启以后，系统能连接网络，继续后面的软件包的安装。
