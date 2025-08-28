---
layout: post
title: 从USB硬盘启动树莓派4B
date: 2021-12-21 08:11:57
categories: ARM Linux RaspberryPi
tags: Archlinux ARM RaspberryPi Raspbian
---

引用1：https://gist.github.com/XSystem252/d274cd0af836a72ff42d590d59647928
引用2：https://archlinuxarm.org/forum/viewtopic.php?t=14672#p64313

应用1是一个大神做的笔记，应用2是ArchLinuxARM2020年底时候对于USB硬盘启动做的讨论，这个帖子在ArchLinuxARM论坛被置顶了。应用1整理了引用2 中关于USB硬盘启动的方法外，还在USB硬盘上使用btrfs文件系统，还做了全盘加密。我这里没有这么多的需求，所以对原文做了一个简化。

另外因为我的树莓派4B是2019年买的，也就是说其eeprom比较早，需要升级，我也把怎么更新这部分内容，做了描述。

## 概述

大约在2019年12月份的时候，搞过一次使用usb硬盘做roofs，原理比较简单，就是从tf卡的vfat分区启动，然后挂载usb硬盘的分区作为rootfs，然后配置cmdline.txt文件就好了。

但是最近这个树莓派滚挂了，原因也很简单，当时使用的是三方LTS的aarch64的内容，后来ArchLinuxARM接管了这个内核，再后来ArchLinuxARM牛B大了，不用LTS的内容，开始为树莓派4B提供与ArchLinux相同的滚动最新内核，并且在树莓派4B的bootloader与内核之间加了一层uboot，然后我的这个树莓派4b就滚挂了。

今天某东新买的tf读卡器到了，就花了一下午的时间把这个研究了一下，终于搞定记录一下。

树莓派4B最新的eeprom更新了bootloader,可以通过raspi-config来做启动顺序的设定。可以设定tf卡启动失败，再使用usb硬盘启动，也可以设定usb硬盘启动失败，再使用tf卡启动。这样一来，我们就可以直接从USB硬盘启动，不再像我2019年时候还是用tf卡的vfat分区做启动。

另外，今天发现最新ArchLinuxARM在启动的时候没法挂载usb硬盘,但是启动以后可以挂载，这样就需要定制一下内核的img，保证在内核加载的时候，相应usb的驱动能被加载。

在开始前，我们需要准备一张tf卡，这个卡要先用来升级树莓派4B，后面再用来定制ArchLinuxARM。

## 升级树莓派4B

我准备直接用2019年时候的那个tf卡，这个卡是16G。我先在我的manjaro xfce里面安装了一个叫rpi-imager的包，他是树莓派基金会官方出的tf卡制作工具的linux版，现在这个工具很牛B了，除了可以刷Raspberry Pi OS（Raspbian），还能直接刷manjaro arm和libreelec。在这个tf卡上刷一个Raspberry Pi OS Lite版，因为我们不需要桌面环境，ssh远程访问就好了。

制作好tf卡以后，加载vfat分区，在里面的根目录下创建一个名为ssh的空文件。linux下可以用下面的命令快速创建。

```bash  
touch ssh
```

将tf卡插回树莓派4b，然后加电启动。在路由器找一个名叫raspberrypi的主机的IP,然后使用如下命令远程登录，默认密码是raspberry。

```bash  
ssh pi@192.168.1.xxx
```
登录后按顺序执行下面的三行命令

```bash  
sudo apt update
sudo apt full-upgrade
sudo rpi-eeprom-update -d -a
```  
这三行命令的第一行是更新本地安装包数据库，第二句是根据最新的本地安装包数据库，更新所有的安装包。我执行完这两行以后，第三行已经不用执行了，从显示的信息看，已经从2019年而eeprom更新到了2021年4月份的版本了。这个2021四月份的版本是稳定版本，如果想换成其他正式发布的版本，好像还可以更新到最新的2021年11月版本。但这与我的目标没有关系了，我也就没有往下升级。

这时树莓派4B的eeprom更新就已经搞完了。我们使用halt命令关机，当树莓派4B的电源灯灭掉的时候，我们先断电，再拔出tf。

## 准备启动TF卡

我们把tf通过读卡器接回manjaro，现在我们可以针对这两个卡进行操作了。因为之前的创建Raspberry Pi OS的时候，tf上面已经有两个分区了，我们现在跳过分区的步骤，开始重新格式化这两个分区。重新格式化vfat是因为ArchLinuxARM使用了uboot，重新格式化ext4是因为ArchLinuxARM的根文件系统与Raspberry Pi OS完全不同。

```bash  
sudo mkfs.vfat /dev/sdc1
sudo mkfs.ext4 /dev/sdc2
mkdir boot
mkdir root
sudo mount /dev/sdc1 boot
sudo mount /dev/sdc2 root
sudo bsdtar -xpf ArchLinuxARM-2021.11-rpi-aarch64-rootfs.tar.gz -C root
sudo mv root/boot/* boot
sudo sed -i 's/mmcblk0/mmcblk1/g' root/etc/fstab
sudo umount boot root
```

最后一行是因为我们安装的是aarch64版本，这个版本貌似mmcblk不是从0开始排的，是从1开始排的。如果是armv7版本的话，是不需要这一行的。使用aarch64版本的好处就是速度快，很多64位的软件可以用，但是坏处是发热量大，我树莓派4B上就安装了一个大散热片。

这样我们就完成了tf的准备，这时可以拔出读卡器，将tf插回树莓派4B。加电前，需要先把USB线断开，这是因为默认的内核img里面usb的驱动，启动时连接USB，在启动以后看不到usb，反而是启动完成再连接usb线能看到usb设备。

我的usb设备不是普通的usb硬盘，而是针对树莓派4b设计的同伴科技的x825笔记本硬盘扩展板，我在上面加了一个本子上拆下来而1T本盘。同伴科技还出来其他的usb硬盘扩展板，你可直接使用m2的ssd，或者3.5寸的台式机硬盘，甚至还能接两个硬盘。

安装准备

在树莓派4b启动以后，我们再去路由上找一个名叫alarm设备的IP。我们使用下面的命令登录。

```bash  
    ssh alarm@192.168.1.xxx
```

下面我们开始准备向USB硬盘上写的系统：

  1. 登录后我们使用su命令切换到root帐号。ArchLinuxARM没有内置sudo，切换成root，后面比较方便。
  2. 修改`/etc/pacman.conf`，去掉`Color`和`ParallelDownloads = 5`前面的注释，然后在`ParallelDownloads = 5`下面加一行`ILoveCandy`。`Color`表示pacman使用彩色界面，`ParallelDownloads = 5`表示pacman使用5个并发下载，能提高下载效率，最后一个`ILoveCandy`是一个隐藏菜单，pacman会使用游戏吃豆的特效来现实进度条。
  3. 修改`/etc/pacman.d/mirrorlist`，这个可以修改成国内中科大镜像或者清华tuna的镜像，速度在我这儿位置是最快的，具体怎么改不细说了，参考 http://mirrors.ustc.edu.cn/help/archlinuxarm.html
  4. 先后执行`pacman-key --init`和`pacman-key --populate archlinuxarm`。
  5. 执行`pacman -Syu`将系统盘滚动更新到最新的版本。
  6. 然后通过命令行`pacman -S uboot-tools rsync`安装两个工具，第一个是uboot工具，用于更新uboot启动配置，第二个是同步工具，将tf上制作完成的系统同步到usb上。
  7. 这个时候我们先重启树莓派4b。

重启后我仍然用ssh登录在切到root帐号。

  1. 然后修改`/etc/mkiniycpio.conf`，在`MODULES=()`的括号中加上`pcie_brcmstb`。保存后执行`mkinitcpio -P`，这样会重新创建一个新的initramfs镜像文件，这将保证内核在启动时支持usb。
  2. 编辑`/boot/boot.txt`。编辑前备份一下这个文件。将`part uuid ${devtype} ${devnum}:2 uuid`这一行注释掉。
  3. 在将下面一行中的`root=PARTUUID=${uuid}`改为`root=/dev/sda2`。然后在`/boot`目录执行`./mkscr`。
  4. 编辑`/etc/fstab`。将`/dev/mmcblk1p0 /boot vfat defaults 0 0`中的`mmcblk1p1`换成`sda1`。
  5. 这时我们连接usb硬盘，连接后通过lsblk查看能否看到/dev/sda设备。
  6. 如果能看到，我们对usb硬盘进行分区，与tf分区类似，第一个分区256MB,类型为c，第二个分区为剩下磁盘大小，类型不变。我们在安装好以后使用交换文件来做交换内存，不使用交换分区。
  7. 回到root帐号的home，创建boot和root两个目录，将`/dev/sda1`挂载在boot上，将`/dev/sda2`挂载在root上。
  8. 执行`rsync --info=progress2 -axHAX /boot/ boot/`和`rsync --info=progress2 -axHAX / root/`，将tf的两个分区同步到usb硬盘的两个分区。然后再执行sync确保磁盘写操作真是完成。
  9. 这时我们就可以关闭树莓派4b，拔电后取出tf，再不拔出usb硬盘的情况下，重新加电启动。这时我们从路由上可以看到，一个叫alarm的设备已经获得ip了。

后续的设置，已经和普通的Archlinux没有什么区别了，设置一下ntp自动更新时间，设置一下当前的时区，设置一下locale，设置一下hostname等等。当然为了winbios名字解析，也可以安装一个samba。

> 2025-08-28 注: 如果不用ArchLinuxARM会更简单。现在已经切换为Ubuntu Core。使用rpi-imager刷一个切换usb优先启动的镜像到usb硬盘，启动一下树莓派，然后在刷Ubuntu Core到usb硬盘就好了。
> 
> 作为服务器来用的话，Ubuntu Core比arch好用啊