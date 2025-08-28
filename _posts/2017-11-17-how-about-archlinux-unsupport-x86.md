---
layout: post
title: Archlinux官方不再支持i686(x86)以后，老机器怎么办？
date: 2017-11-17 15:17:40
categories: Linux
tags: Archlinux
---

新装机的话，可以从archlinux32.org下载纯32位的安装包。

原来archlinux官方的i686装机，可以更换archlinux32的更新服务，方法如下：

1. 先把`/etc/pacman.d/mirrorlist`的内容换成 https://raw.githubusercontent.com/archlinux32/packages/master/core/pacman-mirrorlist/mirrorlist 这个内容。这里面是最新的archlinux32的镜像文件清单，今天镜像服务器数量爆发性增长，是昨天的两倍了，昨天只有4个，今天8个了。国内目前不要选新加坡的那个，死慢，小鬼子的速度最快。
2. 执行`pacman -Syy archlinux32-keyring-transition`来更新证书链。
3. 执行`pacman -Syuu`来做完整升级。
  
但是有两个问题：

1. 是目前archlinux32的包没有archlinux的新，可能得有相当数量的包会提示降级。
2. 是开始第一次会提示你本机缓存的老版本包的数字签名不对，一种解决办法是当提示你的时候，选Y然后删掉原来的包，再-Syuu的时候就会重新下载对的，另一种解决办法是在开始前先运行pacman -Sc据说会清理掉数字签名不对的。

不管咋样，我去重启我的那个机器去了

.

.

.

.

.

.

顺利重启，反正我也不关心是不是出了什么问题。

话说，国内也没谁写这样的Blog了吧

> 2025-08-28 注: 对，也没谁了