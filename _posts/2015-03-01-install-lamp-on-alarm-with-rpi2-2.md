---
layout: post
title: 树莓派2上玩ArchLinux+LAMP(2):TF卡制作
date: 2015-03-01 15:52:10
categories: 技术
tags: ARM Box Linux RaspberryPi MySQL PHP Apache LAMP
---
系列文章：

(1)TF卡制作环境：http://just4fun.cn/?p=725

前一篇写了怎么搞环境，这一节就开始做卡。这一节介绍的内容，对于制作树莓派1和树莓派2的ArchLinuxARM的Root FS，都是一样的。

在准备开始前需要准备好一个好用的读卡器。我之前就被一个不好用的读卡器折腾了一晚上才做好一个卡，不然算上下载的话，10分钟也足够了。

下面开始制作过程：

1. 启动之前我们做好的虚机，确保网络是通的。
2. 使用`wget http://mirrors.tuna.tsinghua.edu.cn/archlinuxarm/os/rpi/ArchLinuxARM-2015.02-rpi-2-rootfs.tar.gz` 下载当前最新版的rootfs，树莓派1可以使用[ArchLinuxARM-2015.02-rpi-rootfs.tar.gz](http://mirrors.tuna.tsinghua.edu.cn/archlinuxarm/os/rpi/ArchLinuxARM-2015.02-rpi-rootfs.tar.gz) 。这两个不能混用，因为树莓派1的ARM处理器是arm5指令集，树莓派2是arm7指令集。也就是说二进制代码不一样。
3. 在电脑上插好带有TF卡的读卡器，然后在vbox虚机的窗口的菜单：设备->分配USB设备菜单里，选择读卡器设备。这时电脑会安装一个vbox的usb设备，资源管理器里面磁盘也会消失，虚机里面会有新设备提示。
4. 确保用`ls –l /dev/sd* `能看到新的sdb，在进行下一步。
5. 使用`fdisk /dev/sdb`进行分区。o命令先清除掉原有分区记录，n命令在创建第一个分区，id默认1，起始扇区默认使用2048，结束扇区使用+100M。在用t命令，将这个分区类型修改为c。再用n命令创建第二个分区，id默认2，起始扇区和结束扇区默认。之后用w命令写入分区信息。
6. 这时在用`ls –l /dev/sdb*`，应该可以看到sdb1和sdb2。
7. 使用`mkfs.vfat /dev/sdb1`格式化第一个分区，然后`mkdir boot`创建这个分区的挂载目录，用`mount /dev/sdb1 boot`挂载第一个分区。
8. 使用`mkfs.ext4 /dev/sdb2`格式化第二个分区，然后`mkdir root`创建这个分区的挂载目录，用`mount /dev/sdb2 root`挂载第二个分区。
9. 使用`bsdtar –xpf ArchLinuxARM-2015.02-rpi-2-rootfs.tar.gz –C root` 命令将rootfs解压缩到root目录。为确保缓存内的数据被写入，可以再执行一个`sync`命令。
10. 再执行`mv root/boot/* boot`，把rootfs里面boot内的文件全部剪贴到boot分区的目录。
11. 这时就可以执行`umount boot root`了。执行完毕拔读卡器就好。

这时你就可以把TF卡查到树莓派2上面开始测试了。插上电源，连好网线，可以直接ping一下alarmpi这个主机名。如果Ping不到的话，可以到家中路由器的dhcp管理里面看看名为alarmpi的名字对应的ip是什么。
