---
title: "Mono于FreeBSD上的试用（1）"
date: 2004-07-10 15:01:00
layout: post
categories: FreeBSD dotnet mono
tags: FreeBSD dotnet mono
---

在看了[luyan](http://blog.joycode.com/5drush)的linux上使用mono的文章，我就开始心痒痒，mono也可以在FreeBSD上面用啊！

这里的朋友应该没几个不知道Linux的，但是对FreeBSD很了解的就不多了。FreeBSD是以BSD4为基础发展起来一个开源的Unix操作系统，使用BSD许可发布。BSD发布许可的内容很简单，就是：可以以任何方式来使用FreeBSD的源码和二进制程序，使用的时候只需声明代码来自FreeBSD。这样使用这个发布许可，你就可以在自己的代码任意使用FreeBSD的代码，而不用交费或者继续开源。这很有一点教科书的意味，恐怕没有谁为教科书上的知识而付过任何费用或者为此而不能申请自己的专利或者版权。

FreeBSD以及整个BSD系列的开源操作系统的风格也同样非常学院派。系统追求稳定可靠的同时，不断改进，对于软件包的发布集中控制。这样在FreeBSD的世界里面，不会有一个软件包会针对不同的FreeBSD版本发布很多个，因为FreeBSD只有一个发布人——就是FreeBSD的发布小组。

FreeBSD内建了很多令人瞠目结舌的机制。最醒目的是一个内置的操作系统模拟器，在这里面可以模拟linux、novell等等i386上面的操作系统，像Linux下面的二进制格式软件（jdk,oracle8/9）几乎都可以直接运行在FreeBSD当中。

由于FreeBSD的这些优秀特性，FreeBSD已经被很多大型企业用于各自的生产环境当中，很多网络设备的嵌入式系统也有FreeBSD的影子。同时FreeBSD也是微软认同的开源操作系统之一，早在2000年，FreeBSD就已经是微软 CLI 1.0 跨平台运行环境示范平台之一。

上面介绍完了FreeBSD，接着说说在FreeBSD上面实现mono和ASP.Net的事情。

我首先查阅了FreeBSD的ports列表，这里面显示ports安装只支持mono-0.97，也不支持mod_mono，看来只好自己安装了。

首先去 http://www.mono-project.com 下载mono1.0的源码，准备编译。