---
title: "ASP.NET通过使用Membership管理用户(1):前言"
date: 2005-12-26 16:21:00
layout: post
categories: aspnet
tags: aspnet
---

### 译者前言

ASP.NETv2与前一个版本之间的一个比较显著的区别就是添加了membership管理。这个是一个显著的特性。希望可以通过MSDN里面的这一篇"Managing Users by Using Membership"来打到抛砖引玉的作用。本文的版权属于MSDN。转载译文请标明出处来自于 ~~http://blog.zhangchi.com.cn~~ 。

### 原著前言

ASP.NET成员可以使你的Web应用有效的管理用户信息。它提供了一些功能，诸如：确认用户，创建和修改成员用户，和管理用户的密码、电子邮件地址之类的用户信息。ASP.NET成员主要用在ASP.NET的Forms验证，但是也可以使用在Web应用的任何地方。

ASP.NET成员使你可以管理你的应用用户验证，并将信息存储到你的数据源当中。因为ASP.NET成员用户提供了成员数据的数据源，所以你不比扩展任何代码就可以读写用户信息。

ASP.NET成员主要有内置的成员Provider组成，它与数据源通信，并由静态的membership对象暴露出成员Provider的功能。你可以在你的ASP.NET代码中调用membership对象来执行用户的确认和管理。

### 内容目录

* Membership的介绍
* 对照Membership与Windows和Passport验证
* Membership对象
* Membership Provider
* 配置ASP.NET应用使用Membership
* Membership的安全性
* 实现一个Membership

> 2025-08-27 注: 20年了，爱转转吧