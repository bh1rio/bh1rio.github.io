---
layout: post
title: 关于树莓派Raspberry Pi Zero W、3B、3B+使用串口控制台的问题
date: 2018-12-20 10:51:53
categories: RaspberryPi
tags: Archlinux
---

收了一个Zero WH，外加一个UPS Hat。接上以后，发现putty使用串口无法登录，于是在网上查来查去，最后搞定。记录一下。

树莓派的SoC有两个UART，一个叫PL011一个叫miniUART。默认扩展插针上的UART是PL011。但是树莓派的ZeroW\3B\3B+和以往的型号不一样，增加了蓝牙，并且默认连接在PL011上，这时miniUART自动连接在扩展插针上。这样的话，如果不修改cmdline.txt和config.txt的情况下，是无法连接串口控制台的。

PL011和miniUART的主要区别在于，PL011是外部的串口模块，有独立的时钟，速率稳定为115200，输入输出缓存会相对大一些。miniUART没有独立时钟，受到core主频的影响。

根据树莓派官方文档 https://www.raspberrypi.org/documentation/configuration/uart.md 的描述，最简单的解决办法是关闭蓝牙，这样PL011会自动切换到扩展插针上。管理蓝牙模块的办法也很简单，在config.txt里面加上

```  
dtoverlay=pi3-disable-bt
```
