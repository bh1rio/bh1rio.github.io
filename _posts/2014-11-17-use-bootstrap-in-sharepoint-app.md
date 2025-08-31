---
layout: post
title: 在SharePoint 2013的SharePoint App中使用Bootstrap
date: 2014-11-17 09:05:50
categories: 技术
tags: SharePoint
---

知乎上有人说“很多审美糟糕的程序员拿到Bootstrap 了以后都以为自己不需要前端了”。但是在没有前端工程师的情况下，还是得用Bootstrap。

查了一下，貌似国内没有人写。老外有写的，一是版本有点老，二是方法麻烦，估计也是强迫症闹的。他非要把bootstrap的css、js、img合并到App自己的相应目录，得到的结果是自己修改css。要知道修改这个有多痛苦。

后来试验了直接在项目中创建一个bootstrap的目录，那些css、js、img都扔这里下面，就全解决了…….目前Napa测试了可用。
