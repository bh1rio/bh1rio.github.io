---
layout: post
title: ArchLinux内核4上面的EDUB EP-N8508GS迷你USB无线网卡
date: 2015-11-07 09:21:31
categories: 技术
tags: Archlinux ARM Linux RaspberryPi WIFI Box
---
在树莓派和PC的ArchLinux的2015.11上，驱动都没有问题。

lsusb显示：

```
Bus 001 Device 004: ID 0bda:8176 Realtek Semiconductor Corp. RTL8188CUS 802.11n WLAN Adapter
```

lsmod显示使用的是8192cu的驱动，使用cfg80211栈。

使用wifi-menu连接的时候，会有ioctl的错误信息，但是不影响连接。
