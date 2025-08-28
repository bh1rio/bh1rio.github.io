---
layout: post
title: Transmission的RPC验证
date: 2020-07-19 10:39:07
categories: Linux
tags: Archlinux
---

Transmission的RPC接口很好用，Transmission-Remote-GUI就是玩pt的利器，但是RPC验证不开启的话，会有一些诡异的行为没有文档描述。比如：

* 不开启验证，TRGUI添加磁链或者种子的时候，会提示下载路径不是绝对路径，但是原生的WebGUI没有问题。
* 不开启验证，使用域名访问（非localhost）的时候，会提示拒绝，建议用ip或者开启验证。

以上行为在Transmission 3.0和TRGUI的5.18上会出现。
