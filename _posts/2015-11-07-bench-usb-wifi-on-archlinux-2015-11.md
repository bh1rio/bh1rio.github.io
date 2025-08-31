---
layout: post
title: 关于ArchLinux 2015.11上迷你USB无线网卡的对比测试
date: 2015-11-07 10:44:54
categories: 技术
tags: Archlinux ARM Linux RaspberryPi WIFI Box
---

今天中午到了昨天收的7个网卡，加上原来手里的水星MW150US 2.0，一起在树莓派2B上的ArchLinux ARM 2015.11进行了测试，结果总结如下：

1. 完美的网卡

**RTL8191SU芯：**

磊科net-core NW360 300M无线网卡

lsusb信息：`Bus 001 Device 006: ID 0bda:8172 Realtek Semiconductor Corp. RTL8191SU 802.11n WLAN Adapter`

参考《[树莓派1&2 ArchLinux ARM 2015.11目前最完美的USB无线网卡](http://just4fun.cn/2015/11/07/the-best-usb-wifi-for-archlinux-arm-2015-11.html)》

2. 需要手动驱动的网卡

**MT7601U芯：**

必联B-Link BL-D88 150M迷你USB无线网卡

lsusb信息：`Bus 001 Device 007: ID 148f:7601 Ralink Technology, Corp. MT7601U Wireless Adapter`

参考《[ArchLinux内核4上面的B-Link BL-D88迷你USB无线网卡](http://just4fun.cn/2015/11/07/archlinux-with-kernel-4-set-b-link-bl-d88.html)》

3. 自动驱动但是报错的网卡

**RTL8188CUS芯：**

EDUB EP-N8508GS 150M迷你USB无线网卡

lsusb信息：`Bus 001 Device 008: ID 0bda:8176 Realtek Semiconductor Corp. RTL8188CUS 802.11n WLAN Adapter`

参考《[ArchLinux内核4上面的EDUB EP-N8508GS迷你USB无线网卡](http://just4fun.cn/2015/11/07/archlinux-with-kernel-4-set-edub-ep-n8508gs.html)》

**RTL8188EUS芯：**

水星Mercury MW150US 2.0 150M迷你USB无线网卡

lsusb信息：`Bus 001 Device 009: ID 0bda:8179 Realtek Semiconductor Corp. RTL8188EUS 802.11n Wireless Network Adapter`

COMFAST CF-WU810N 150M迷你USB无线网卡

lsusb信息：`Bus 001 Device 009: ID 0bda:8179 Realtek Semiconductor Corp. RTL8188EUS 802.11n Wireless Network Adapter`

COMFAST CF-WU720N 150M迷你USB无线网卡

lsusb信息：`Bus 001 Device 009: ID 0bda:8179 Realtek Semiconductor Corp. RTL8188EUS 802.11n Wireless Network Adapter`

参考《[ArchLinux内核4上面的水星MW150US v2.0迷你USB无线网卡](http://just4fun.cn/2015/11/07/archlinux-with-kernel-4-set-mw150us-v2-0.html)》

4. 无法驱动的网卡

COMFAST CF-WU825N 300M迷你USB无线网卡

lsusb信息：`Bus 001 Device 004: ID 0bda:818b Realtek Semiconductor Corp.`

COMFAST CF-WU725B 蓝牙4.0和300M迷你USB无线网卡

lsusb信息：`Bus 001 Device 005: ID 0bda:b720 Realtek Semiconductor Corp.`

测试环境：

1. 根据ArchLinuxARM 2015.11新生成的RaspberryPi 2 B环境

2. 在`pacman -Syu`更新到最新的环境

3. 用`pacman –S dialog wpa_supplicant crda`安装最新的wifi组件

4. 修改`/etc/conf.d/wireless-regdom`文件，去掉`WIRELESS_REGDOM="CN"`之前注释用的`#`。
