---
layout: post
title: 给ArchLinux配置NetBIOS/WINS协议的hostname解析
date: 2019-09-23 06:57:35
categories: Linux
tags: Archlinux
---

这个需求的背景是，博主使用树莓派作为开发服务器，使用windows环境内做客户端完成开发。树莓派在连接不同的网络的时候，动态获取的IP每一次都变化，在代码中动态调整比较烦人。如果能支持NetBIOS的话，那么就可以直接通过主机名，在不同的网络环境中都使用名字来访问树莓派。

一般的Linux的桌面环境这么做都不存在什么问题，但是像ArchLinux这样的极简系统就需要自己配置NetBIOS服务在局域网内广播主机名。一般Linux环境都有现成的Samba可用，而Samba服务端就内置了NetBIOS/WINS服务端，这样我们安装好Samba，启动相应服务就好了。

在ArchLinux当中，可以通过如下步骤解决：

1.安装Samba包

```bash
pacman –S samba
```

2.从`https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD` 获取最新版的smb.conf放在/etc/samba目录下。

3.启动winbind服务

```bash
systemctl enable winbind
systemctl enable nmb
```

这样，即使不启用Samba服务，我们先在也可以使用NetBIOS和WINS协议找到这个树莓派了。这个办法在Archlinux的PC和树莓派上都适用。
