---
layout: post
title: 在Arduino IDE 1.6里配置ATtiny44/45/84/85
date: 2016-01-04 16:23:22
categories: 技术
tags: Arduino ATtiny AVR
---

刚才顺手有看到了支持ATtiny44/45/84/85的Arduino支持，于是顺手再写下来。这个支持来自[Damellis’es ATtiny cores](https://github.com/damellis/attiny/)，看具体内容前要先修改一下分支，目前有一个ide-1.6.x-boards-manager的分支。

当然直接安装也比较简单，在Arduino IDE的File->Preferences的Additional Boards Manager URL里面填上`https://raw.githubusercontent.com/damellis/attiny/ide-1.6.x-boards-manager/package_damellis_attiny_index.json`这个地址。这时在Tools->Boards->Board Manager的最西面会看到下图的内容：

![](/images/2016/01/image-1.png)

这时，选择最新的版本，然后点击Install按钮就好。然后在Tools->Board里选择ATtiny以后，你就能看到下图菜单的样子：

![](/images/2016/01/image-2.png)

祝各位玩的愉快：-）
