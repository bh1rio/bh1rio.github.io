---
layout: post
title: 关闭内核信息输出控制台
date: 2020-09-30 03:34:11
categories: ARM Box Linux
tags: Archlinux ARM Linux
---

关了内核的audit信息，还是有电压之类的信息在不停的输出，找了raspberry pi官方的文档，说修改config.txt文件的告警级别，但是实测不太管用，于是准备彻底关闭内核信息的输出。

查了一下，把cmdline.txt里面的console=tty1删掉了，内核信息就不输出控制台了。如果想看，可以保留输出到串口，连接串口查看。
