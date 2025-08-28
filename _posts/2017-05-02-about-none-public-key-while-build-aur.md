---
layout: post
title: 解决在使用AUR编译pgadmin4的安装包的时候遇到找不到公钥的问题
date: 2017-05-02 06:57:53
categories: 未分类
tags: 
---

提示RSA的ID为某个值的公钥找不到。这个时候，需要用pgp命令下载公钥。

命令为pgp –recv-keys 公钥

参考链接：

* http://www.cnblogs.com/daemon369/p/3204020.html
* http://www.2cto.com/kf/201703/607171.html
