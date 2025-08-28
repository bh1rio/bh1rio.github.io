---
layout: post
title: Archlinux的时间同步
date: 2020-07-23 02:22:09
categories: Linux
tags: Archlinux
---

现在Linux主机的最佳实践是硬件时钟设置为UTC时间，然后设置自己的时区。但是如果是一台之前没有安装过Linux的主机，就会有一个问题，怎么精确设定时间。当然，如果联网的条件下，NTP是最简单的办法。以前这么做都是通过ntpd包带的ntpclient来实现。现在多了一个选择：`systemd-timesyncd`。

启用过程很简单，现在修改`/etc/systemd/timesyncd.conf`，去掉`NTP=`前面的注释，然后在后面填上`time.windows.com`这个服务器。然后使用`timedatectl set-ntp true`起作用这个服务。

之后可以用`timedatectl status`开查看当前系统的时间状况。也可以用`timedatectl timesync-status`来查看时间同步的情况。

