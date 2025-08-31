---
layout: post
title: ArchLinux内核4上面的水星MW150US v2.0迷你USB无线网卡
date: 2015-11-07 09:34:59
categories: 技术
tags: Archlinux ARM Linux RaspberryPi WIFI
---
在树莓派和PC的ArchLinux的2015.11上，驱动都没有问题。

lsusb显示：

```
Bus 001 Device 004: ID 0bda:8179 Realtek Semiconductor Corp. RTL8188EUS 802.11n Wireless Network Adapter
```

lsmod显示：

使用的是8188eu的驱动，使用cfg80211栈。但是在插卡的时候不会加载cfg80211，只有在wifi-menu之后，才会加载。

使用wifi-menu连接的时候，会有ioctl的错误信息，但是不影响连接。在wifi-menu，里面看不到信号评分或者信号的分贝提示。dmesg会有错误信息。

补充：

1. COMFAST CF-WU810N的lsusb和lsmod信息一致。

2. COMFAST CF-WU720N的lsusb和lsmod信息一致。
