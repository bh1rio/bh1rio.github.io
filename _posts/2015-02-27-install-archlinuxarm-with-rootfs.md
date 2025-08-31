---
layout: post
title: 树莓派和树莓派2的ArchLinuxARM的img文件
date: 2015-02-27 11:42:40
categories: 技术
tags: ARM Box Linux RaspberryPi
---

之前我发货一篇《[修改树莓派ArchLinux分区的大小](http://just4fun.cn/?p=648)》，现在这篇文章过时了。

原因是树莓派网站不在提供ArchLinuxARM的img文件，响应的ArchLinuxARM网站也不以img格式来发布新版本。ArchLinuxARM直接提供了RootFS包，需要找一个Linux的机器对tf卡进行分区，再将RootFS解压缩到tf卡。这样就不再需要重新调整分区大小了。

今天树莓派2已经到手，顺手下载了树莓派、树莓派2、Cubieboard、Cubieborad2的ArchLinuxARM的2015.2的包，找时间做一个纵向的大评测。今天不上照片了，照片还在手机里……

ArchLinuxARM 2015.2的Pi和Pi2的内核是3.18.2，sun4i和sun7i的内核是3.4.103。这个纵向大测试会相当的值得期待。

话说当初在用Cubieboard做评测的时候，ArchLinuxARM的内核还是3.0.58，据说是因为Allwiner不出新驱动……现在看A10芯片还是沾了A20芯片的光，才有新内核可用。树莓派不存在这个问题，内核都是最新的，话说是不是过段时间就有Kernel 4用了呢？

期待啊~~~
