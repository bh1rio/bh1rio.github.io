---
layout: post
title: D630安装ArchLinux
date: 2014-04-03 10:20:03
categories: 技术
tags: Archlinux
---
U盘的安装盘制作，参考前文：http://just4fun.cn/?p=685。安装过程参考Arch Linux Wiki的[Beginner’s Guid](https://wiki.archlinux.org/index.php/Beginners%27_guide)。

1. 开机使用U盘启动以后，直接选择“Boot Arch Linux (x86_64)”。机器已经支持64位了，又是4G内存，没有理由还选择i686的方式了，启动之后会自动登录的root账号。

2. 由于咱也不懂其他的语言，暂时不修改键盘和语言之类的内容，直接开始配无线。我的这个D630是4965无线网卡，当前版本的Arch直接支持，使用“ip link”命令已经可以看到网卡的设备名为wlp12s0，所以直接使用“wifi-menu wlp12s0”连接无线。如果没提示直接出来了，那么就是已经连接成功，这个时候可以ping一下某个知名网站看看。说个题外话，有人说[www.baidu.com](http://www.baidu.com) 的存在意义就是用来ping网通不通的，很有意思10年前大家都是在ping [www.sina.com.cn](http://www.sina.com.cn)，突然有一天大家发现自己和别人都开始ping [www.baidu.com](http://www.baidu.com) 了，这是一个有意思的现象。

3. 接下来准备存储，其实就是分区。U盘启动以后，机器的硬盘设备名为sda，U盘的设备名为sd2。我习惯使用fdisk，所以接下来就是`fdisk /dev/sda`。先删除所有存在的分区，再创建两个主分区。第一个分区为4G，主当交换分区，剩下的都给/。好处就是省事。创建完成以后，将sda1的类型改为82，将sda2设置为可启动，然后保存退出。fdisk删除使用d命令，创建使用n命令，修改类型使用t命令，修改启动标志使用a命令，查看分区表使用p命令，查看帮助使用m命令，保存退出使用w命令。

分区之后是格式化，使用`mkfs.ext4 /dev/sda2`格式化根分区，使用`mkswap /dev/sda1`格式化交换分区，使用`swapon /dev/sda1`启用交换分区。

格式化完毕使用`mount /dev/sda2 /mnt将根分区挂在当前目录的/mnt位置。

4. 在向sda2灌rootfs之前，先修改pacman的镜像列表。当前镜像列表的最后一项就是163的镜像服务器，可以把前面的都删掉。如果你有多个其他的镜像网站可选，可以先ping一下，选一个最快的。使用`vi /etc/paman.d/mirrorlist`开始编辑。vi怎么用自己去网上查吧

5. 修改好以后，使用`pacstrap –i /mnt base`来安装基本系统，也就是灌rootfs。后面是一路回车，就可以完成。从屏幕提示看，可以知道Arch不是使用光盘上的安装包，而是从刚才修改的mirrorlist里面的镜像服务器来下载安装需要的文件。

6. 安装完成以后，使用`genfstab –U –p /mnt >> /mnt/etc/fstab`来生成系统的fstab文件。

7. 接下来就可以使用`arch-chroot /mnt /bin/bash`将当前shell的根目录换成/mnt了。这时我们可以看到提示符已经和刚才不一样了。

8. 接下来在更换过来的根目录里面分别设置`/etc/locale.gen`文件并使之生效，然后修改`/etc/locale.conf`。这个是设置新系统的语言环境。使用`vi /etc/locale.gen`命令打开这个文件，然后把需要使用的语言前面的#号去掉，我这里使用的是`en_US.UTF-8`，另外我还打开了`zh_CN.UTF-8`，执行`locale-gen`生成locale。然后使用`echo LANG=en_US.UTF-8 > /etc/locale.conf`来生成这个文件。

9. 由于中国人都是使用国际标准键盘，所以键盘和控制台字体就都不修改了，直接使用默认设置。

10. 接下来执行`ln –s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`设置当前时区为上海。然后使用`hwclock --systohc --utc`来设置系统硬件时钟为UTC模式，也就是说机器BIOS时间代表格林威治时间。根据Arch Linux Wiki的说法，这是建议设置，也可以设置为localtime，但是会有一些一直bug，而且没有计划修改这些。我很郁闷，我用了这么多年电脑，BIOS里面的时间都是本地时间。没办法，改吧。

11. 核心模块这个时间点不配置，跳过。

使用`echo myhostname > /etc/hostname`设置机器名。hosts文件不需要修改，使用默认就好。

接下来网络配置这块比较重要，因为需要安装一些组件，一边重启后可以继续使用wifi-menu。这需要执行`pacman –S iw wpa_supplicant dialog wpa_actiond`安装相应的程序包。相关配置重启之后再做。

使用`mkinitcpio –p linux`创建ramdisk环境。

使用`passwd`修改root的密码。

使用`pacman –S syslinux`安装bootloader，然后执行`syslinux-install_update –i –a -m`来使syslinux生效。之后使用`vi /boot/syslinux/syslinux.cfg`修改bootloader启动时加载的分区。

之后就可以重启了，执行“exit”返回之前的shell，执行`umount –R /mnt`去掉/mnt挂载的sda2，然后就可以“reboot”了。

重启之后，可以创建新用户，或者安装其他软件。我是用命令`systemctl enable netctl-auto@_wlp12s0_.service`打开了自动登录无线。

> 2025-08-31 注: 1.现在可以用ventoy启动iso了，比当年简单了好多。2.我的d630被媳妇开窗户雨淋了。