---
layout: post
title: 自动安装Archlinux的脚本
date: 2017-12-04 16:18:33
categories: Linux
tags: Archlinux
---

最近受ArchLinux官方的Dockerfile的启发，做了一个Archlinux的安装脚本，发布在 https://github.com/bh1rio/archlinux-install

里面的脚本，可以在安装iso启动以后，wget后来运行。这个脚本也适用Archlinux32，但是需要修改mirroslist文件中的镜像服务器地址，目前ustc和yun-idc的mirror还没有ArchLinux32的镜像。

如果你希望干预修改root的密码，你可以注销掉其中的passwd行，不修改问题也不大，因为login的时候root不需要密码。login进去再修改密码就好了

当然你也可以fork自己的版本然后修改。比如我的hptc小机器，就可以加入raid相关的代码。

如果你的网络够快，5分钟就可以准备好一个干净的Archlinux。（嗯，我这里是500Mb的光纤![Smile](/images/2017/12/wlEmoticon-smile.png)）
