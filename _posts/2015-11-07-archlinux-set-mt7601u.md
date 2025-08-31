---
layout: post
title: 在ArchLinux上驱动mt7601u无线usb网卡
date: 2015-11-07 07:34:05
categories: 技术
tags: Archlinux ARM Linux RaspberryPi WIFI
---

上一篇《[在ArchLinux ARM下驱动RTL 8188eu无线网卡](http://just4fun.cn/?p=828)》对网卡不好用，很是郁闷。所以这次整了一堆无线usb网卡来测试。今天很高兴，完美驱动了mt7601u网卡，当然这个过程不是一帆风顺，不然也就不必要写这么一篇blog了。

先说使用这个片子的网卡：

必联(B-Link) BL-D88 http://item.jd.com/1154411.html

必联(B-Link) BL-150SM http://item.jd.com/1154451.html

传说小米的随身wifi也是这个片子，但是我手头没有小米的随身wifi，所以读者自己测试吧

再说驱动为什么不是一帆风顺：我在pc和arm的ArchLinux上测试这个网卡的时候，发现插上设备以后，系统没有新增网卡设备，lsusb发现识别正常，lsmod发现驱动正常，dmesg发现加载firmware时，没有找到firmware文件。于是自己去 http://www.mediatek.com/en/downloads1/downloads/mt7601u-usb/ 这里下载了一个最新的，你不想注册信息的话，可以从我的百度盘下载http://pan.baidu.com/s/1hqpWmGG 。我共享的这个文件，不需要改名字，直接sftp上传，然后复制到/lib/firmware里面，重启pc或者树莓派就好了。

sftp可以使filezilla client。
