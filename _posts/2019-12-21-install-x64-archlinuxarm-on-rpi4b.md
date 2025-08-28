---
layout: post
title: 树莓派4上的64位Archlinux
date: 2019-12-21 06:47:28
categories: ARM Box Linux
tags: Archlinux RaspberryPi
---

前两天终于咬牙跺脚收了同伴科技的X825，这是因为树莓派4终于支持了USB3.0，能基本把硬盘的性能跑出来了。顺便研究了一下，现在树莓派4上面的64位Linux，基本上可以确定现在树莓派4可以当做小型服务器来耍了。

首先，树莓派4是aarch64架构的arm处理器，4G内存，千兆网络，USB3.0接口，基本可用了。其次，Docker Hub上的服务器应用也开始支持aarch64了，甚至像mariadb、mongodb和openjdk的docker官方镜像只支持arm的aarch64架构。

网上查了一段时间，对比了树莓派爱好者基地的64位debian和第三方出的64为archlinuxarm，觉得还是喜欢archlinux，于是写写怎么在树莓派4上跑64位的archlinuxarm。

感觉archlinuxarm网站论坛里面的讨论，找到了一个三方出的树莓派4的64为archlinuxarm的rootfs，地址是 https://olegtown.pw/Public/ArchLinuxArm/RPi4/rootfs/ ，挑一个最新的，按照archlinuxarm官方树莓派4的安装教程 https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4#installation 来安装就好了。安装好以后，连接有线网络，可以在路由器的dhcp设备列表里面找到设备的ip，这时候远程登录就好了。

安装好以后需要做一些官方教程里面没有的额外设置，首先要用nano来编辑`/etc/resolv.conf`，添加一行`nameserver 8.8.8.8`。这是因为这个rootfs没有安装vi包，其次没有设置dns服务器。如果我们需要改成静态ip,需要修改`/etc/systemd/network/eth.network`。

如果需要使用netbios访问树莓派4，可以参考我之前写的 http://just4fun.cn/2019/10/23/archlinux-set-netbios-wins.html

如果需要使用文件做交换内存，可以参考我之前写的 http://just4fun.cn/2018/02/25/make-mariadb-docker-img-for-x86.html

这个时候可以开始配置X825上面的硬盘作为rootfs。我是专门从狗东买了一个容量最小的tf卡，按照前面的介绍安装好archlinuxarm，分区并格式化/dev/sda1，然后直接修改/boot/cmdlin.txt就好了。但是在树莓派爱好者基地的64位debian貌似这么做不好用，可能是因为它用了树莓派上面UFEI导致的，没有深入研究。

硬盘接好启动以后，用fdisk先给硬盘创建一个分区，把格式化好ext4的分区mount在`/mnt/newdrive`，然后执行命令`rsync -avx / /media/newdrive`把tf卡的rootfs同步到硬盘上。这个步骤在树莓派爱好者基地的64位debian上也不好用。之后修改cmdline就好了。

重启之后，使用df -h看看根fs是不是挂在sda1上。

另，这个三方的roofs可以用pacman更新archlinuxarm官方的aarch64软件包，但是因为官方没有aarch64的树莓派内核，所以需要自己从 https://olegtown.pw/Public/ArchLinuxArm/RPi4/kernel/ 和https://olegtown.pw/Public/ArchLinuxArm/RPi4/firmware/ 下载最新的内核和firmware。此外这个网站还提供了5.4的内核，但是因为树莓派官方的内核只有4.19的代码，所以我没敢尝试。

> 2025-08-28 注: 现在可以用树莓派官方的镜像工具来将树莓派的eeprom升级支持usb优先启动，然后直接把镜像写道USB的硬盘。而且现在换成了Ubuntu Core。这个做服务器还是比Arch稳定，不怕滚挂了。