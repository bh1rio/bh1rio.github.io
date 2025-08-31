---
layout: post
title: 在ArchLinux ARM下驱动RTL 8188eu无线网卡
date: 2015-11-05 13:21:53
categories: 技术
tags: 8188eu Archlinux ARM Linux RaspberryPi Box
---

在2013年4月的时候，我曾写过一篇《[在Cubieboard的ArchLinux下驱动RTL8188eu无线网卡](http://just4fun.cn/?p=650)》。现在两年半以后，因为ArchLinux ARM的升级，所以那片帖子的里面的内容已经过时了。但是根据访问统计看，还有人在访问，而且我现在自己也想把自己树莓派上面的网线换成无线，所以有了今天这篇的内容。今天的这个内容，我在树莓派1B+、树莓派2B以及x86的环境中都做了测试，目前看实验现象似乎都是一致的。水星Mercury的MW150US网卡有多个版本，我手里的这个是MW150US v2.0。

在2013年的时候，当时ArchLinux ARM的内核还是Linux 3，但是现在ArchLinux和ArchLinux ARM的内核都已经是Linux 4了，而且RTL的驱动程序也在升级，所以情况也是有变化的。

先说说现状：

目前RTL 8188eu的驱动，在ArchLinux和ArchLinux ARM的内核里面都已经内置了，插上USB以后，使用lsmod会看到有一个r8188eu的驱动在，但是无论使用wpa_supplicant还是wifi-menu，都无法连到无线路由器。翻墙查了相关的搜索结果以后，大部分都在建议使用 https://github.com/lwfinger/rtl8188eu/tree/v4.1.8_9499 的新驱动，据说老的驱动是3下面的驱动，在4里面无法很好的工作。

编译并安装驱动：

首先用`pacman –S base-devel git dkms iw wpa_supplicant dialog crda linux-raspberrypi-headers`安装必要的组件。这其中`base-devel`是编译需要的工具链，`git`是代码获取工具，`iw`、`wpa_supplicant`、`dialog`是配置无线网的工具，`dkms`是动态内核配置工具。`crda`能设置无线网卡的频率范围，`linux-raspberrypi-headers`是编译驱动所需要的头文件。

然后获取代码`git clone –b v4.1.8_9499 https://github.com/lwfinger/rtl8188eu.git`，这会将一个稳定的版本下载到本地。下载后可以先修改`rtl8188eu`中的`Makefile`文件，其中`CONFIG_POWER_SAVING`的内容修改为`CONFIG_POWER_SAVING = n`，目的是关闭省电功能。然后就可以使用`make`或者`dkms`来编译了，具体可以参考github的页面上的帮助。这两种做法会有一个区别，区别是`make`会自动在`/etc/modprobe.d/`内创建一个`50-8188eu.conf`文件，他会把内核中的`r8188eu`模块加入blacklist，我们自己可以编辑这个文件，并加入一行`options 8188eu rtw_power_mgnt=0`，给驱动送参数，来关闭相关的电源管理。

结果：

目前看按照上面的操作完成驱动安装以后，某些时候会工作的比较好，`dmesg`里面已经没有错误信息了。但是说某些时候，是因为不确定原因的某些时候工作的不好。据说最完美的情况是在x64的情况下，据说github上维护代码的这个作者，他用的是这个环境。

还有就是目前看，ArchLinux的作者和使用者确实激进，因为从搜索结果看，大部分是ArchLinux的用户在提问。另外，还有相当多的用户是和我一样在树莓派上使用。

我目前的想法是换一个usb网卡试试。没准换过几个网卡之后，我会写一个迷你usb无线网卡的评测，哈哈

再加一句:ArchLinuxARM论坛里面推荐的dkms-8188eu的方法并不好用，也已经测试了。
