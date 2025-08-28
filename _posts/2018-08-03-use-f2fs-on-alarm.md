---
layout: post
title: 在ArchlinuxARM中使用F2FS文件系统
date: 2018-08-03 02:15:04
categories: ARM Linux RaspberryPi
tags: Archlinux
---

做tf的系统（我的系统就是archlinux）需要安装f2fs-tools。

针对ArchlinuxARM官方的安装过程，替换mkfs.ext4为mkfs.f2fs

目前树莓派的最新内核，以及aarch64最新内核都会支持这个文件系统，不需重新编译内核

系统第一次启动以后，需要安装f2fs-tools，默认的跟目录包不包含它。resize.f2fs和fsck.f2fs会依赖这个包。

对于f2fs能对tf有多少提升，现在很多人意见不统一，至少他是针对tf设计的。
