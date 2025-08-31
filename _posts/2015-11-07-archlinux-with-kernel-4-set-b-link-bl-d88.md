---
layout: post
title: ArchLinux内核4上面的B-Link BL-D88迷你USB无线网卡
date: 2015-11-07 10:07:04
categories: 技术
tags: Archlinux ARM Linux RaspberryPi WIFI Box
---
在树莓派和PC的ArchLinux的2015.11上，驱动都没有问题。

lsusb显示：

```
Bus 001 Device 004: ID 148f:7601 Ralink Technology, Corp. MT7601U Wireless Adapter
```

lsmod显示：

使用的是mt7601u的驱动，使用mac80211和cfg80211栈。

dmesg的时候会提示firmware文件mt7601文件无法读取，可以用《[在ArchLinux上驱动mt7601u无线usb网卡](http://just4fun.cn/2015/11/07-archlinux-set-mt7601u.html)》文章中的方法解决。解决之后，dmesg信息中会有firmware加载成功的信息。

使用wifi-menu连接的时候，没有任何错误，接入点后面是其信号强度的分贝值。
