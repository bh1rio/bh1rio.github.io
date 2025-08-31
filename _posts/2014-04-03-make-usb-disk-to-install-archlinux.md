---
layout: post
title: ArchLinux USB安装盘制作
date: 2014-04-03 08:04:46 -0000
categories: 技术
tags: Archlinux D630 Linux
---
前段时间收了一个集成显卡的D630，翻箱倒柜又找了2G的内存，凑足4G内存，自带的120G的7200转硬盘，正好装个Arch来玩。说实话，D630除了壳子塑料以外，集显的机器真的是码农利器，想当年用的那几台都不是自己的，用过就归还了，这次在水木的版里看到出的，600块钱就收来玩了。一个是玩Linux，一个是玩串口给台子写频，杠杠的。

手头没找到空的刻录盘，研究了一下怎么制作ArchLinux的USB安装盘。在ArchLinux的Wiki里面找了一下，找到一个[USB Flash Installation Media](https://wiki.archlinux.org/index.php/USB_Flash_Installation_Media)的说明。因为这是D630是第一台专职Linux机器，所以就研究了一下这文档里面在Windows下怎么做的内容。

Windows下有三个方法，归根节点还是两个方法，一个是使用专门的启动U盘制作工具，一个是使用dd。Windows下的专门工具他推荐的是[Universal USB Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) ，这个工具好处是不需要安装，也不大，带配置向导，界面也不复杂，还能自动帮你下载iso。但是我测试不好用，不知道是里面的syslinux的版本太老还是什么情况，反正是用我新下载的archlinux 2014.04.01的iso制作的U盘卡在了syslinux的步骤。

dd这个方法和linux上基本一致，那文档里分成了两个方法，一个是安装cygwin，一个是直接下载windows版的dd。我是直接下载来一个windows版的dd，马上就有专门的linux机器了，谁还玩cygwin啊，呵呵。[下载地址](http://www.chrysocome.net/dd)

命令也很简单：dd if=archlinux-2014.04.01-dual.iso of=\\\\.\g: bs=4M

其中[\\\\.\g](file://\\\\.\\g):标示这是我的G盘。如果你的杀毒软件正在扫描U盘的话，那么写入U盘可能失败，没事，等会儿再试就好。写入完成以后，U盘上会有两个分区，一个64兆的fat32，还有一个是rootfs。rootfs一般不会沾满你的U盘，除非你的U盘1G大小都没有。

剩下的就没有什么了，插到D630启动就好，如果直接启动到硬盘了，那就重启修改BIOS启动顺序就好。

> 2025-08-31 注: 改用ventoy吧