---
title: "Mono于FreeBSD上的试用（4）"
date: 2004-07-29 15:07:00
layout: post
categories: FreeBSD dotnet mono
tags: FreeBSD dotnet mono
---

终于狠下心来将那块SCSI的硬盘取下，为了mono~~~~~~

取下来硬盘之后，立刻就可以安装FreeBSD5.2.1了。

现阶段已经发布的最新的FreeBSD版本4.10和5.2.1都不能正常安装mono-1.0的ports。
据mono的ports的制作人讲mono的ports在4.10上不能安装是因为libc里面有一个死锁错误，导致在安装dll的时候随机性的死锁。
而mono还不支持在5.2.1上面安装，是因为mono需要的一个内核特性5.2.1还没有。
这样如果安装mono的ports需要升级成5.2-current。根据我的经验，升级后使用ports安装没有任何问题。

下面在安装xsp和mod_mono的时候遇见的问题比较大：
* xsp不能正确地make。
* mod_mono可以正常编译安装，但是ModMono.dll却不能正常编译。

在mono实现的ASP.NET的方案当中，xsp和ModMono.dll起着很重要的角色，就是起到真正运行一切ASP.NET程序的作用，而mod_mono只在apache当中拦截所有的被看作到ASP.NET请求，转发至ModMono.dll或者xsp去。

接下来要解决的就是正确编译xsp或者modmono.dll，我想我要解决这个问题，还是先从make文件如何编写入手，或者你们谁给我一个编译好的？