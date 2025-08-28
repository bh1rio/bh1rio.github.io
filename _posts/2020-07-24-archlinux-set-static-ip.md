---
layout: post
title: Archlinux安装阶段的静态IP修改
date: 2020-07-24 06:15:52
categories: Linux
tags: Archlinux
---

办公室的网络需要授权才能访问互联网，server有不需要授权的网段，但是archlinux的iso启动的时候默认是dhcp获取的ip，这就需要将ip改为不需要授权的网段。研究了archlinux的wiki，找到了修改方法。

archlinux的iso是用的是systemd-networkd这个服务来设置iso启动的网络设置，这就需要修改/etc/systemd/network/20-ethernet.network。

首先，去掉DHCP相关设置：删除`[DHCP]`段，删除`[Network]`的DHCP=yes

然后，加静态IP设置，在`[Network]`段加上：

```
Address=192.168.1.2/24
Gateway=192.168.1.1
DNS=114.114.114.114
```

最后，用`systemctl restart systemd-networkd`重启网络服务。
