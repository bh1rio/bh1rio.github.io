---
layout: post
title: OMV5安装extras插件后性能统计图片无数据问题的解决
date: 2021-04-16 01:38:46
categories: Linux
tags: nas omv
---

最近把蜗牛星际矿渣不知道为啥不知道同时4块12T，于是把系统换成了OMV5，但是用脚本装完了omv5-extras插件以后，系统信息->性能统计 里面的图片全成空的了。由于OMV用的少，5的资料也少，不知道从什么地方下手解决。

最近没事就搜一搜，查一下，最后在omv-extras的github的问题反馈里看到有人也反应这个问题。按照其中的解决办法，能解决问题。看描述应该omv-extras的安装脚本关闭了collectd服务，解决办法也简单，用systemctl打开并启动collectd服务就好了
