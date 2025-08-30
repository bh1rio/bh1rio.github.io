---
layout: post
title: ATtiny13的Core13在Arduino IDE 1.6上的配置
date: 2016-01-04 15:57:55
categories: 技术
tags: Arduino AVR
---

目前在Arduino IDE里面能搞的最低处理器应该是ATTiny13了，ATtiny有几个选择，但是ATtiny13只有一个Core13选择。

Core13的下载地址：http://sourceforge.net/projects/ard-core13/ 。本文成文的时候，最新版本是022版本，而且这个版本有了一个Arduino IDE 1.6版本的专门包，推荐下载这个。我目前的测试环境是1.6.5，但最新的版本已经是1.6.7了。这是因为我也在玩另一个ATtiny85的小板子，叫DigiSpark，它的程序不兼容1.6.5之后的版本，所以……就不升级了。

Core13在Arduino IDE 1.6上安装很简单，只需把压缩包中的attiny13这个文件夹解压缩到你`<我的文档>\Arduino\hardware`这个目录下就好了。关闭再重新打开Arduino IDE，你就能在Tools->Board菜单里找到Attiny13的选项了。下图里面可以看到我配置好的样子，上面还有DigiSpark的选项。另外还有一个国产atmega328p克隆版LGT8F328D做的Larduino的选项。

![](/images/2016/01/image.png)
