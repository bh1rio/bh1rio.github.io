---
layout: post
title: ArchLinux笔记本电脑合盖不休眠的方法
date: 2017-09-03 16:21:44
categories: Linux
tags: Archlinux
---

找了一个N270处理器的小上网本跑ArchLinux当开发服务器，结果发现合上屏幕就会休眠，于是祭起搜索引擎神器，在ArchLinux的Wiki宝典里面找到了如下的办法：

* 修改`/etc/systemd/logind.conf`

其中：

* HandlePowerKey：按下电源键后的动作
* HandleSleepKey：按下挂起键后的动作
* HandleHibernateKey: 按下休眠键后的动作
* HandleLidSwitch：合上笔记本盖后待机

动作可以是：ignore、poweroff、reboot、halt、suspend、hibernate、hybrid-sleep、lock 或 kexec。

话说自己用还是喜欢ArchLinux，云上的话CentOS也可以忍受 
