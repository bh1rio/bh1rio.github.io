---
layout: post
title: netctl开启自动连接wifi
date: 2018-12-20 12:10:25
categories: Linux
tags: Archlinux
---

首先使用wifi-menu连接过一些wifi，这样在/etc/netctl下会有一些链接文件。然后安装wpa-actiond包，再开启netctl-auto@wlan0服务。

1. `pacman –S wpa-actiond`
2. `systemctl enable netctl-auto@wlan0`

这样重启以后，就会从已有的连接文件中，选取信号最强的那个wifi自动连接。
