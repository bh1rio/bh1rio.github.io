---
layout: post
title: 树莓派1&2 ArchLinux ARM 2015.11目前最完美的USB无线网卡
date: 2015-11-07 09:09:33
categories: 技术
tags: Archlinux ARM Linux RaspberryPi WIFI Box
---
在我这次买的一堆USB无线网卡里面，磊科NW360这个是唯一的不需要做任何操作就可以使用的无线网卡，内部应该是RTL8191SU芯片。

lsusb的信息是

```
Bus 001 Device 004: ID 0bda:8172 Realtek Semiconductor Corp. RTL8191SU 802.11n WLAN Adapter
```

lsmod显示驱动为r8712u，使用cfg80211栈。目前，从dmesg看，无任何错误信息。
