---
layout: post
title: Pomelo.EntityFrameworkCore.MySql和Boolean类型
date: 2021-08-27 00:52:51 
categories: dotnet
tags: dotnet
---

最近在折腾dotnet 6的webapi，结果发现tinyint(1)在从数据库表创建数据对象实体的时候，没有被转换成Bool类型。百度没找到答案，在github的问题清单里面有人提到过这个问题，发现这个问题好像和MySqlConnector有关。

解决方案出人意料，在数据库连接字符串里面，加上“TreatTinyAsBoolean=true”就好了。主要有两个场景，一个是从表创建对象实体时命令行的连接字符串，一个是创建好实体以后的数据库连接字符串。
