---
layout: post
title: Atmel Studio 7.0 (build 634)在升级Visual Studio 2015.1之后错误的解决
date: 2016-01-04 10:03:40
categories: 技术
tags: AVR
---

翻墙查了一下，有Atmel的员工提供了一个方法，见 [链接](www.avrfreaks.net/forum/visual-studio-2015-update-1-incapacitates-atmel-studio-7) 。

方法如下：

1.去nuget下载 https://www.nuget.org/api/v2/package/System.Collections.Immutable/1.1.36
2.按照zip文件解压缩下载的nupkg文件，找到`System.Collection.Immutable.dll`等两个文件。
3.解压缩到`C:\Program Files (x86)\Atmel\Studio\7.0\Extensions\Application`。这个可能根据你安装Atmel Studio的位置不一样而不一样。

> 注:
>
> 1. 你要是不知道Visual Studio 2015.1是什么东东的话，忽略过上面的内容。
> 2. 你需要确认在 `<UserDir>\AppData\Roaming\Microsoft\AppEnv\14.0\ActivityLog.xml`中有`System.Collection.Immutable`的错误信息，这个错误信息并不会Atmel Studio 7提示的错误信息中出现。
