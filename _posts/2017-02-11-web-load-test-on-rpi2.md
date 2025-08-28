---
layout: post
title: 今天闲的蛋疼给树莓派上nginx的默认页做压力测试
date: 2017-02-11 11:38:42
categories: Linux Web
tags: Archlinux nginx
---

树莓派2安装最新的ArchLinuxARM，然后安装标准的nginx。压力源使用VS2015中测试项目的WebLoadTest。

第一次没调nginx的工作进程数，第二次调成4个工作进程，于是…….真相如下：

![7413978647@chatroom_1486811612135_38](/images/2017/02/7413978647@chatroom_1486811612135_38.png)

![7413978647@chatroom_1486811913517_83](/images/2017/02/7413978647@chatroom_1486811913517_83.png)

最惨的是我自己的pc跑满了 

![0C915302](/images/2017/02/0C915302.png)

![7413978647@chatroom_1486811501740_85](/images/2017/02/7413978647@chatroom_1486811501740_85.png)
