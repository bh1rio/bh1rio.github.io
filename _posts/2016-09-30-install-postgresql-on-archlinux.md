---
layout: post
title: 在ArchLinux中安装PostgreSQL
date: 2016-09-30 02:51:08
categories: 技术
tags: Archlinux Linux PostgreSQL
---

这个可能是我Blog里面第一篇使用Open Live Writer写的内容，目前其本版为0.6。

前段时间摔伤，把手里的工作交接了一下，顺便开始研究一些之前腾不出时间做的研究。这次是在ArchLinux上安装PostgreSQL。研究了一下PostgreSQL的文档，写的很细，但是无从下手。研究了一下ArchLinux的Wiki，基本过程写了，但是还有问题，自己折腾了两天才搞定，特此记录一下。

1. 首先还是要安装postgresql安装包。

```bash
pacman –S postgresql
```

2. 安装包搞定以后，会自动创建postgres账号。按照ArchLinux的要求，需要修改这个账号的密码，作为开发环境可以跳过。然后su成这个账号，做数据库的初始化。因为postgresql是以这个账号运行的，所以数据库初始化，一定要su成这个账号。

```bash
su postgres
initdb –locale $LANG -E UTF8 –D ‘/var/lib/postgres/data’
exit
```

3. 初始化完成以后，会创建好配置文件和系统库。接下来编辑配置文件。配置文件都在刚才的数据目录内。

先修改`postgresql.conf`文件，去掉listen_address前面的注释符，并将内容修改为*号，表示监听所有的IP。

再修改`pg_hba.conf`文件，添加`host all all 192.168.1.0/24 md5`，表示允许某个网段以md5编码的方式验证用户登录。

4. 修改完成就可以注册服务和启动服务了。

```bash
systemctl enable postgresql
systemctl start postgresql
```

5. 启动以后需要修改管理账号的密码

```bash
psql –U postgres
postgres=#\password postgres
```

6. 这样就安装完成，可以使用远程的pgAdmin 3试试能否连接到服务器了。
