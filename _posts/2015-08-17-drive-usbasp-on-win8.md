---
layout: post
title: 在Win8.1下驱动USBasp
date: 2015-08-17 10:01:29
categories: 技术
tags: Arduino usbasp
---

手里有一个两个能给8951下载程序的USB ISP。一个插上机器，被直接识别为HID设备，另外一个找不到驱动。使用自带的驱动，windows 8.1提示驱动没有签名。网上查了一下，两种解决方案，一种是去掉Windows 8的强制驱动签名，一种是使用签名的驱动。

如果想使用签名驱动的话，可以下载[Zadig](http://zadig.akeo.ie/)。下载运行以后，在1的位置会显示未驱动的设备，我这里显示的USBasp。如果你有多个未驱动的设备，可以从里面选一个。在2的位置，选择libusb-win32。这是因为其自带驱动是libusb0，选择WinUSB可能会给你安装libusb1。然后点击按钮Install WCID Driver。

![](/images/2015/08/image.png)

安装好以后，在设备管理器里面看我的USBasp就是这样的。

![](/images/2015/08/image1.png)

说个题外话，你如果玩过用电视棒玩过SDR#的话，你会发现现在最新版的SDR#自动下载的安装包里也会有这个Zadig。并且也是用他来给电视棒安装SDR#需要的驱动的。
