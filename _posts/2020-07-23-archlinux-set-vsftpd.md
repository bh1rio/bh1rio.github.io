---
layout: post
title: Archlinux安装ftp服务
date: 2020-07-23 02:29:16
categories: Linux
tags: Archlinux
---

前两天安装的transmission服务，下载的内容只能通过sftp拿回来。后来发现sftp服务传输效率不高，在需要安全的情景下也还能忍，但是在家里内网的情况下，千兆带宽只跑20%，cpu负载就满了，还是专门配置一个明文的ftp好。

网上看了一下，vsftpd用的最多，而且看archlinux的wiki，这个貌似也是最简单。我就选这个了。其实我要求不高，不用开匿名，不用单独账号列表，使用系统账号就好，能把下载的内容删除，这么多就好。过程如下：

1. `pacman –S vsftpd`
2. 编辑`/etc/vsftpd.conf`
3. 去掉`write_enable=YES`前面的注释
4. 去掉`local_enable=YES`前面的注释
5. 使用`systemctl`启用并启动`vsftpd`

这就可以打完收工了。
