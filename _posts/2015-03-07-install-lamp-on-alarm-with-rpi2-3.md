---
layout: post
title: 树莓派2上玩ArchLinux+LAMP(3):安装MariaDB、Apache和PHP
date: 2015-03-07 07:33:21
categories: 技术
tags: Apache ARM Box Linux MySQL PHP RaspberryPi
---
系列文章：

(1)TF卡制作环境：http://just4fun.cn/?p=725

(2)TF卡制作：http://just4fun.cn/?p=727

MariaDB是在Oracle收购MySQL以后，社区做的开源分支。目前ArchLinux已经把MariaDB作为了MySQL的默认替代，我们这里也以MariaDB作为替代。MariaDB和MySQL协议兼容，内部应用也保持原样，所以除了在安装的时候不一样以外，后面的步骤的都类似。Apache和PHP就不说了，大家都懂的。

1. 安装和配置MariaDB

(1)首先使用`pacman –Syu`升级系统上的现有的组件。

(2)接着执行`pacman –S mariadb`。这个命令会安装MariaDB服务器端、客户端命令行工具和客户端库。

(3)使用`systemctl enable mysqld.service`命令启用MariaDB服务。使用`systemctl start mysqld.service`立即启动MariaDB。

(4)启动以后，使用`mysql_secure_intallation`命令启用安全配置向导。按照向导回答问题就好。具体问题代表什么请自己查询MariaDB或者MySQL的资料。

(5)如果你不需要开启root的远程访问，这个时候你的MariaDB就已经安装好了。如果你需要开启root的远程访问，那请往下继续。

(6)执行`mysql –u root –p`，之后会提示你输入密码。密码是刚才安全向导中设置过的。除非你没设置。

(7)先执行`use mysql;`然后执行`grant all privileges on *.* to 'root'@'%' with grant option;`

(8)再执行`grant all privileges on *.* to 'root'@'%' identified by 'mypass' with grant option;`需要注意的是不要缺少最后面的分号。上面mypass是针对远程时候root的密码，可以改成自己的。可以单独设立。执行两边是因为第一遍生成了一个没有密码的账号，第二个开启密码。

(9)之后exit退出，就全部OK了。

2. 安装配置Apache和PHP

把Apache和PHP一起写是因为可以利用pacman提供依赖管理，在安装PHP的时候，自动安装好Apache。

(1)执行`pacman –S php-apache`安装apache和php的所有组件。

(2)执行`vi /etc/httpd/conf/httpd.conf`配置apache

用

```
LoadModule mpm_prefork_module modules/mod_mpm_perforl.so
```

替换

```
LoadModule mpm_event_module modules/mod_mpm_event.so
```

这是archlinux的wiki中要求的，原因我没去研究。

再在最后部分添加

```
LoadModule php5_module modules/libphp5.so
Include conf/extra/php5_module.conf
```

这会将php5的相关配置包含到httpd.conf中。

(3)执行`vi /etc/php/php.ini`配置php

我这里保持默认就可以了

3. 测试

测试其实非常简单，写一个phpinfo页面就好了。
