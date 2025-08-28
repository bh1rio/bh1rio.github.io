---
layout: post
title: 关闭ArchLinuxARM控制台的audit输出
date: 2020-09-30 02:13:09
categories: ARM Linux Box
tags: Archlinux ARM
---

以前没研究linux写屏，这些输出还无所谓，最近决定研究一下怎么关闭这个输出。

alarm的论坛有人回复了两种方法，一种直接关掉audit，一直是关掉输出。

关掉audit可以在/boot/cmdline.txt最后面加audit=0

关掉输出可以`systemctl mask systemd-journald-audit.socket`
