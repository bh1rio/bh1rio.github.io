---
layout: post
title: 在Virtual Box上安装ArchLinux简明过程
date: 2016-07-09 05:14:32 -0000
categories: 技术
tags: Archlinux Linux
---

1. 准备：

下载最新的iso文件，准备虚机，测试网络。

2. 使用iso启动虚机，测试网络是否可用。

3. 分区和磁盘准备： sda1为交换分区，大小与内存相同，sda2为剩余空间。

分区：`fdisk /dev/sda`

格式化主分区：`mkfs.ext4 /dev/sda2`

格式化交换分区： `mkswap /dev/sda1`

启用交换分区：`swapon /dev/sda1`

加载主分区：`mount /dev/sda2 /mnt`

4. 修改当前使用的镜像服务器，我是修改为163的镜像。

```bash
vi /etc/paman.d/mirrorlist
```

5. 灌rootfs。包括基础和开发两部分包。

```bash
pacstrap –i /mnt base develop
genfstab –U –p /mnt >> /mnt/etc/fstab
```

6. 切换root

```bash
arch-chroot /mnt /bin/bash
```

7. 修改locale信息

修改`/etc/locale.gen`，再执行`locale-gen`

执行`echo LANG=en_US.UTF-8 > /etc/locale.conf`

8. 修改时区和local时间

```bash
ln –s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc –utc
```

9. 修改机器名

```bash
echo myhostname > /etc/hostname
```

10. 修改密码

```bash
passwd
```

11. 安装bootloader

```bash
pacman –S syslinux
syslinux-install_update –i –a –m
vi /boot/syslinux/syslinux.cfg
```

12. 退出重启

```bash
exit
umount –R /mnt
reboot
```

> 2025-08-30 注: 当前底5步需要按照下面连接修改 https://just4fun.cn/2019/10/23/some-change-of-archlinux-install.html