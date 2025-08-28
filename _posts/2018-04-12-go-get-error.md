---
layout: post
title: 关于go get失败的处理
date: 2018-04-12 03:33:40
categories: Go
tags: Go
---

几个方案，基本上需要能科学上网，或者有化外vps

方案1：

有一条虚拟专用网络能科学上网。

方案2：

走代理，go get会在失败的时候，走环境变量http_proxy或https_proxy指定的地址。ssh能提供sock5代理，可以用privoxy转成http代理

方案3：

直接把需要go get在化外vps上执行，然后将生成的相应目录打包拉回。但是Windows上这个方法需要手动把bin和pkg目录都删掉，只留src，重新编译windows的二进制和静态库

以上方法1在windows上实验通过，方案2和3在linux上实验通过。

> 2025-08-28 注: 现在go已经自定义源，国内也有不少源镜像了。