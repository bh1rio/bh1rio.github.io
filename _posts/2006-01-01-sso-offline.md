---
title: "SSO的假脱机问题解决"
date: 2006-01-01 13:03:00
layout: post
categories: SharePoint
tags: SharePoint SSO
---

前两天SPS的数据库服务器坏了，数据被迁移到了备用数据库。这两天把原来在SPS上做的应用都检查了一遍，发现一个使用SSO的Webpart不能正常工作了，表现就是SSO不能正常取出数据，成脱机状。

找不到原因，有怀疑是迁移数据库或者安装了SPS2003的SP2造成的，于是重新安装了SPS2003而且没有安装其SP2。但是问题依旧，于是开始分析我的代码。最终发现是我的Webpart的问题：界面上显示从SSO当中获取的帐号，是在调用一个WebService并得到正常返回以后才显示，而当数据库迁移以后，WebService的数据连结没有更改过来，WebService没有返回一般性的错误代码；而我的代码只对WebService正常返回和一般性错误信息进行捕获。这样造成了我的Webpart的假脱机状态。

最终可以确定SPS2003的SP2不会对SSO造成这样的影响，但是不能确定数据库的迁移会不会对SSO造成影响。