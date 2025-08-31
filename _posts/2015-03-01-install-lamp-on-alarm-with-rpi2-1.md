---
layout: post
title: 树莓派2上玩ArchLinux+LAMP(1):TF卡制作环境
date: 2015-03-01 14:06:00
categories: 技术
tags: ARM Box Linux RaspberryPi
---
之前写过树莓派官网不再提供ArchLinuxARM的img下载，我们可以直接从ArchLinuxARM网站下载树莓派或者树莓派2的Root FS，相应的也就不想再需要在把img刷到TF卡以后在调整分区大小。那么我就来总结一下制作TF卡的过程。第一步需要先准备制卡环境。

img文件有其方便的一面，比如img文件有win32的制作程序，我们在现有的windows环境制作就好了。但是改为Root FS之后，就需要准备一个Linux环境来制作TF卡。

由于大多数人不一定有现成Linux环境，或者不想装双系统，或者现有Linux环境使用麻烦，所以我们这里介绍一个使用VirtualBox（下面一律简称为vbox）安装ArchLinux环境来制作。我之前就是有一个Ubuntu的vbox虚机，但是制作的时候不管是不是使用sudo，都会提示我权限不足，索性Ubuntu虚机删掉，安装一个全新的ArchLinux虚机。

我之前写过在D630上安装ArchLinux，其实做vbox的虚机，与之过程类似，但是由于制作TF卡的要求比较低，我们可以简化这个过程，然后加上必要工具安装的过程。下面就是安装过程：

1. 先下载Virtual Box的最新版本。地址：https://www.virtualbox.org/wiki/Downloads。只要不是太旧的版本就好，因为太旧的版本不支持挂载USB设备。当前版本是4.3.22。
2. 下载最新的ArchLinux的iso文件。当前版本是2015.2。这里推荐从 http://mirrors.tuna.tsinghua.edu.cn下载。这里是清华学生网管协会的镜像网站，不管是ArchLinux还是ArchLinuxARM都有镜像，速度还不错。
3. 在安装好Virtual Box以后，在里面创建一个ArchLinux虚机，32位的就好，内存建议1G以上，不过估计512MB就足够了。
4. 为虚机挂载之前下载的ArchLinux的iso之后启动，会进入到ArchLinux的LiveCD环境，先ping一下外网，看是不是网络已经通了。我们的这个环境创建，会直接从网络来完成安装。一般只要不是vbox虚机的网络配置有问题，应该是直接可以ping通的，ArchLinux已经默认支持虚机里面的虚拟网卡了。
5. 我们使用`ls –l /dev/sd*`命令，应该可以看到sda和sdb。sda是LiveCD的根系统，已经分区。sdb是虚机的硬盘，还没有分区。
6. 我们直接使用`fdisk /dev/sdb`格式化虚机的硬盘。先用n命令创建一个分区，默认使用分区id为1，使用默认起始扇区2048，结束位置使用+4G，在用t命令将这个分区类型改为83。这个分区是作为swap分区。
7. 接着我们在用n命令创建第二个分区，id默认为2，起始扇区和结束扇区都是默认，类型也不需要改变。这个分区是用作根存储。然后使用w命令保存分区信息。
8. 使用`mkswap /dev/sdb1`命令来格式化这个交换分区，然后使用`swapon /dev/sdb1`起用这个交换分区。
9. 使用`mkfs.ext4 /dev/sdb2`命令来格式化这个分区。然后用`mount /dev/sdb2 /mnt`将挂载到文件系统上。
10. 编辑LiveCD上的`/etc/pacman.d/mirrorlist`文件。这里面是pacman的镜像列表，我们只留下清华这个系统，或者163的镜像。vi编辑器怎么使用这里就不介绍了。
11. 在编辑完以后，使用`pacstrap –i /mnt base`来向刚才创建的分区灌入Root FS，按照屏幕提示操作就好。整个过程我这里大约花了不到10分钟，这个时间会根据带宽和选择的镜像不同，时间长短也不同。
12. 在上一步结束之后，使用`genfstab –U –p /mnt >> /mnt/etc/fstab`命令，来生成新系统上的fstab文件，这里面会包括之前我们创建的交换分区。
13. 接下来执行`arch-chroot /mnt /bin/bash`来启用新的shell环境，这个时候已经切换到我们之前做好Root FS的sdb2来作为我们的文件系统根。显示新的提示符之后，标示执行成功。
14. 之后编辑`/etc/locale.gen`文件，只留下`en_US.UTF-8`即可，然后执行`locale-gen`命令。
15. 执行`echo LANG=en_US.UTF-8 > /etc/locale.conf`来生成`locale.conf`。这一步和上一步，都是来生成系统使用的语言和编码。如果之后这个系统会被用来跑桌面系统，同时还使用中文环境，可以把zh_CN.UTF-8加上。
16. 执行 `ln –s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`。这会为时区设置创建一个软连接到北京时间。
17. 执行`hwclock –systohc -utc`来将vbox虚机的bios时间改为格林威治时间。这个是ArchLinux建议的设置。由于我们已经设置了时区信息，所以系统显示时间还是会使用北京时区来显示的。
18. 执行`echo myhostname >/ect/hostname`来设置当前虚机的机器名。
19. 执行`mkinitcpio –p linux`来创建ramdisk环境。
20. 使用`passwd`来修改新系统的密码。
21. 使用`pacman –S syslinux`命令，安装syslinux。syslinux是新系统的bootloader。安装成功以后执行`syslinux-install_update –i –a -m`这会更新新系统硬盘分区启动扇区信息。
22. 修改`/boot/syslinux/syslinux.cfg`文件，这里面是syslinux加载内核文件的配置信息。我们的新系统，在自己启动以后，根文件系统的分区名字会变成sda2，所以把里面加载内核文件的路径位置的分区改为sda2。
23. 这个时候执行exit命令，回到之前的shell环境。执行成功后，提示符会变成原来的样子。
24. 执行`umount –R /mnt`，然后执行reboot。
25. 看到系统关闭的时候，在vbox的虚机菜单中，将之前挂载的iso去掉，使之从虚机自己的虚拟硬盘启动。
26. 重启后，使用root账号用之前修改的密码登录。
27. 可以ping一下外网看看网络是不是通的，如果没有通，执行ip link看看提示信息。如一般情况会有两个网卡，一个是lo，这个是换回软网卡，一个是enp0s3。或者是和enp0s3类似的名字。这个就是我们网卡的设备名字，使用dhcpcd enp0s3来启动这个网卡上面的dhcp client。如果想每次自动启用dhcpcd或者使用静态域名，请查询ArchLinux的Wiki。在提示信息过后，回到提示符以后，可以再试试ping一下。
28. 网络连通以后，使用pacman –S dosfstools命令，安装格式化dos分区的命令集。这是因为我们的树莓派和树莓派2的TF卡会有一个100M的fat分区。

到此，这个虚机环境已经可以为我们来制作树莓派和树莓派2上面的TF卡了。当然如果你要是玩其他跑ArchLinuxARM的板子的话，例如:Cubieboard1/2/3，也可以使用这个环境来制作TF卡。
