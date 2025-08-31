---
layout: post
title: ArchLinux上开启SSH的Tunnel
date: 2015-04-08 06:16:16
categories: 技术
tags: Archlinux ARM Box RaspberryPi
---
最近单位的网络的飞鱼星打开了，很多网站上不去，于是想在家里的树莓派2上把SSH的Tunnel打开。  
  
修改起来是很简单，用`vi /etc/ssh/sshd_config`编辑sshd的配置文件，找到`AllowTcpForwarding yes`这一行，然后去掉注释，然后保存。

这时候重启就树莓派就好了。
