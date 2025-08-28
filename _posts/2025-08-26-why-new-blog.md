---
title: "为什么要把Blog迁移到Github Pages来"
date: 2025-08-26
layout: post
categories: 未分类
tags: 
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

至于为什么是博客八世，得从我写Blog开始说起。 这段反复写了好几次，实在是回忆不清楚了。

第一世应该是在aspcool网站的多人blog上，貌似是.Text的代码。上次blog搬家时回忆，aspcool的飞鹰还在做比特币算力出租，现在却卖保险了。可叹。

第二世应该是在2004年，宿舍接了ADSL，机器上装了个oblog。从aspcool上迁移了13篇。印象中oblog是威海叶开写的。在威海那两年，还去他公司好几次。

第三世应该是在2006年，换成了dasBlog。dasBlog算是一个全功能的Blog程序，trackback之类都支持了。

第四世是2008年换到了Windows SharePoint Services 3.0上，是因为其支持Windows Live Writer离线写作。同时还是SharePoint MVP的缘故。

第五世是因为实在受不了家里ADSL总是断断续续了，正好朋友托管了买了个VPS，就在他机器上部署了个BlogEnginee.NET。

第六世是2010年的时候，哥们的VPS不续了，于是在香港找了个支持WordPress的PHP空间，部署了第一个WordPress。这次迁移的比较顺利，因为BlogEnginee.NET到WordPress有迁移工具。

第七世是2020年9月的时候，因为有个梯子，于是从香港的空间迁移到了日本的梯子。

现在是第八世。