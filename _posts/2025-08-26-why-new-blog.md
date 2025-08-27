---
title: "为什么要把Blog迁移到Github Pages来"
date: 2025-08-26
layout: post
---

今天算是把Github Pages的Blog搭起来了，虽然还需要优化，但是已经可以往里面填东西了。

为啥我要把原来wordpress的blog迁移过来呢，有以下几个原因:
* Windows Live Writer不能在能Linux上用，但是我现在除了玩游戏都不用Win了，要把写Blog用的素材复制到Win再写有点麻烦，就懒得写了。
* 之前的wordpress需要php和mysql，这两个都需要更新，但是由于跑在docker里面，更起来太麻烦。
* wordpress的`html rich editor`对于coder来讲，表现能力远不如Markdown.
* 之前的那个主机贵，想换更便宜的主机，但是便宜的主机配置低，带宽也低，纠结了一年还是下定决心给它关了。
* 看到[BH1RLW](https://scateu.me)用Github Pages做的Blog，又觉得这种方式不花钱，还能用markdown写Blog，通过git来发布也挺好，就开始研究JekyII

本来准备用导入工具导入wordpress的内容，回头看了一下以前写的内容，发现还挺有意思。
这要是用工具导入的话，估计以后也不会专门的看一遍了，就想还是手动导入吧。
这个工作量有点大，但是反正也不忙，慢慢手工转，看着20年前的自己，还是挺有意思的。

刚才还发现一个意外之喜，Github Pages自动给配上了SSL证书，挺好。

至于为什么是博客五世，得从我写Blog开始说起。

我大概是2004年开始写blog，在之前想写不知道写到哪里。

第一次写Blog是在blog.aspcool.com，aspcool站长飞鹰是我在古城热线的茶秀论坛结识的开发者网友，那时流行多人Blog，飞鹰要求我去常驻。于是我发了第一个Blog。根据2006年5月13日的博客记录，aspcool上面在2004年一共写过13篇。

第一个自己的Blog也差不多是那时候在自己家的机器上搭的。那时候家里的机器上是Windows，ADSL还都是公网IP，就用oblog搭了第一个Blog。这个是博客一世。

博客二世是用的dasBlog，大概是2005年10月换过来的。oblog好像不更新了，和当时流行的博客程序相比也缺少一些看上去不错的功能，就直接换了过来。

博客三世应该是基于WSS 3(Windows SharePoint Services 3.0)的Blog模块。从Blog的记录看，是在2008年的5月的时候。之前已经用SharePoint的Wiki模块做了一个SharePointWiki网站。

博客四世就是wordpress这版。