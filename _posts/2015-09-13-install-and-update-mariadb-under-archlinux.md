---
layout: post
title: 新版ArchLinux上MariaDB的安装和升级
date: 2015-09-13 09:08:41
categories: 技术
tags: Archlinux MySQL
---

最近在ArchLinux上安装MariaDB的节奏和以前有了一些变化。如下：

安装

1. `pacman –S mariadb`
2. `mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql`
3. `systemctl enable mysqld`
4. `systemctl start mysqld`
5. `mysql_secure_installation`

升级（在较大的升级以后，比如5.0升级到10.0或者10.升级到10.1）**

```bash
mysql_update –u root –p
```

为root添加远程访问

```bash
mysql -u root -p
MariaDB> CREATE USER 'root'@'%' IDENTIFIED BY 'some_pass';
MariaDB> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
MariaDB> quit
```