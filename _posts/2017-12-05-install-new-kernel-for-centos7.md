---
layout: post
title: CentOS7安装新内核
date: 2017-12-05 09:22:08
categories: Linux
tags: centos
---

CentOS的包相对还是很保守，没有新内核，没有新软件，也就没有功能。现在4.14的内核已经进入LTS序列了，CentOS还是3.10的内核，捉急

特地研究了一下怎么升级CentOS 7的内核，简单的说CentOS的库里面没有，装其他仓库的，比如elrepo.org里面的过程如下：

```bash
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
yum --enablerepo=elrepo-kernel install kernel-ml
```

写这个blog的时候，已经可以安装4.14.3内核了，后面需要修改grub默认使用的内核：

先`vi /etc/default/grub`，改为`GRUB_DEFAULT=0`

然后重新生成grub的配置文件

```bash
grub2-mkconfig -o /boot/grub2/grub.cfg
```
