---
layout: post
title: 使用ArchLinux的AUR
date: 2017-02-08 09:09:12
categories: Linux
tags: Archlinux
---

Archlinux的AUR里面有很多非官方的软件包，但是需要自己编译，编译前还有很多相应的准备工作。需要先安装base-devel这个安装包的组，然后还要安装git。另外还要准备一个非root的账号，并具备sudo的权限。

1. 当前使用root身份安装必须的文件：

```bash
pacman –S base-devel git
```

2. 使用root身份用`visudo`命令添加`tom ALL=(ALL) ALL`，这里tom就是那个非root账号。
3. 使用`su tom`的方式切换到tom用。
4. 使用`git clone`的方式拿取安装包的信息文件，这会为包安装创建一个文件夹。
5. 进入这个文件夹，然后使用makepkg –si。这会自动下载依赖的安装包，下载依赖的文件，编译这些文件，并制作安装包。然后会问你tom这个账号的密码，密码正确以后，会以root权限来安装刚才做好的安装包。

利用这个可以解决mkinitcpio时候aic94xx和wd719xx两个firmware确实造成的报错。
