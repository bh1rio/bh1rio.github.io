---
title: "Mono于FreeBSD上的试用（3）"
date: 2004-07-14 15:06:00
layout: post
categories: FreeBSD dotnet mono
tags: FreeBSD dotnet mono
---

昨天，将前次安装的mono-1.0又重新作了编译，问题依旧。于是又用ports编译了mono-0.97。但是仍然不能顺利安装。问题是相同的：在向GAC里面安装各种动态链接库的时候！

我自己手动编译的mono在安装第一个dll的时候就出现了问题，ports编译的mono-0.97安装dll出问题的点是随机的。

我自己手动编译的mono在安装dll时候，有2个ltmono进程，而且总是处于poll状态。ports编译的mono-0.97安装dll的时候，只有一个mono进程，并且是RUN状态，CPU占用率也很高（最高到99%），但是很长时间（6个小时左右）没有反应，但是可以用Ctrl+C中断。

在[mono社区](http://www.gotmono.com)里面也看到有人报告mono官方发布的给FedoraCore2的安装rpm不能安装。google上面显示的资源也给人感觉mono并没有让dotNET的开发人员有太强列的兴趣，而开源社区的人对dotNET也没有太大的兴趣。

这次使用之后可能要间隔一段时间，才能在进行更深一步的测试了。时间大约是在周末。