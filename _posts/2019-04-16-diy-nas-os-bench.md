---
layout: post
title: 小NAS系统评测
date: 2019-04-16 10:55:10
categories: 未分类
tags: nas
---

最近因为收了两个星级蜗牛的小NAS机器，计划一个上开源的NAS系统，一个上黑QNAP体会一下NAS+HTPC，所以对开源的NAS系统做了一个对比评测。

先后在vbox里面安装了，FreeNAS，OMV，Openfiler，RockStor，EasyNas，还有国产的U-NAS：

1. FreeNAS是基于FreeBSD，内部界面最酷，支持中文，但是内部功能也相对高冷。貌似没有插件系统。
2. OMV是基于Debian的系统，功能基本全面，插件也足够丰富，最不满意的是没有内置文件浏览器，这个稍有点尴尬。
3. Openfiler是基于rPath这样一个Linux系统，功能和FreeNAS差不多。
4. RockStor是貌似基于CentOS，没有中文界面，只有最近本的功能。
5. EasyNas是基于OpenSUSE，也是没有中文界面，只有最基本的功能。
6. U-NAS比较惊艳，基于Debian，3.16的Linux内核，界面也是Synology和QNAP模仿桌面的界面，和类似App商店的插件安装模式，难得的是还有开源的Web上Office、Note的插件，Transmissions也定制过，更好支持多用户，而且页面也集成了transmission-web-ui，使用上舒服不少。

因为家里Synology已经有了一个ds-716+，一个ds-115，所以Synology已经用的比较熟悉了。所以又在小NAS机器上跑了一个黑QNAP，感受了一下。

综合排名，从好用程度来讲，Synology适合普通家用和SOHO一族。QNAP对应功能也都有，但是感觉比Synology差一些，但是HTPC功能还是不错，但是推荐不用内置的HD_Player，直接用KODI。字幕和解码都比小米盒子之类要强大。小米盒子使用usb 3.0的有线网卡以后，相对QNAP的HTPC功能来讲，主要还是差在字幕和解码上，当然也可能找到更好的安卓App换到小米盒子上。

开源的NAS系统还是OMV更好，可以自己装X来跑KODI，单纯对比功能已经基本上和商业产品差不多了，但是界面有点丑。U-NAS界面和功能都不必OMV差，但是暂时还没有文档描述怎么上KODI，但是因为其基于Debian，估计也能上。其他那几个开源的NAS，我觉得还是算了。

> 2025-08-28 注: 现在又有了一个飞牛NAS，但是还没有用过。现在在用Synology的MailPlus，把outlook替换了，真香。这篇里面还有一个没有评估到，就是硬盘的升级和迁移。这个也很重要。