---
layout: post
title: 介绍两个用于SharePoint的JavaScript资源
date: 2015-06-18 01:29:00
categories: 技术
tags: JavaScript SharePoint
---

最近一直在写SharePoint托管的SharePoint App，只能使用JavaScript来写，加上又都是异步，写起来很痛苦。昨日无意中点开CodePlex以后，发现首页的MOST POP里面介绍了crudeSP，就打开看了一下，发现是好东西。于是又在Codeplex里面找了一下，结果又找到一个好东西CamlJs。

crudeSP包装了SP.js原有的接口，提供了一个更简单的列表和文档库的增删改查接口，还有一个简单的Caml构建器。

CamlJs则就是一个专门的Caml构建器，使用起来很像Linq的的语法，甚是流畅。

他们的地址分别是：

* http://crudesp.codeplex.com/

* http://camljs.codeplex.com/

记录下来，以备后用。
