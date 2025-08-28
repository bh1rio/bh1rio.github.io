---
layout: post
title: 微雪的SPI液晶屏在ArchlinuxARM上的设置
date: 2018-08-08 01:21:15
categories: ARM Box Linux RaspberryPi
tags: Archlinux ARM RaspberryPi
---
我之前的一堆树莓派都找不到了，但是翻出来了一个带微雪3.5寸SPI液晶屏的B+，有点古董。正好前段时候收了一个HDMI的3.5寸液晶屏，顺手对比一下，再写一个配置教程。

微雪的这个屏叫3.5A，应该是有好几个版本了，我手里这个是V3，但是微雪淘宝店里的照片已经不一样了。好在驱动还是一样的。微雪还有一个3.5B，是IPS液晶的面板，也视角会更大。另外还有一个3.5 HDMI产品，也是IPS的面板。这三块屏都是480*320的分辨率。

这三块屏的区别是，HDMI那块带一个驱动芯片，1920的信号输出也能直接显示，模糊而已。因为使用HDMI，一般的img都不需要驱动，另外HDMI的带宽要好，显示速度要快。SPI的这两块，由于数据带宽低，屏幕上更新的内容多了以后，会有明显的刷屏。而且因为SPI不是标准的视频接口，所以需要微雪的接口驱动才能工作。

相应的价格也是3.5HDMI最高，3.5A最便宜，我手里这两个屏，正好一头一个。

微雪网站资料很丰富，3.5A的页面如下：http://www.waveshare.net/wiki/3.5inch_RPi_LCD_(A) 这里面提供了一驱动包，一个安装好驱动的raspbian的镜像，以及一个说明文档。这个文档说明了驱动包怎么用，以及内置驱动的img怎么做tf卡。驱动包地址为 http://www.waveshare.net/w/upload/3/34/LCD-show-180331.tar.gz

我看了一下驱动包怎么安装，也打开了LCD35-show这个脚本，发现这里面基本上两部分内容，显示编译驱动，然后配置控制台驱动和x的驱动。正好看到包里面有编译好的驱动，至少在这个B+上目前工作正常，下面就说说ArchlinuxARM上怎么配置。

1.在驱动包的根目录下有一个`waveshare35a-overlay.dtb`文件，把这个文件复制两次到你archlinuxarm的boot分区的overlays目录下，一次保持原名，一次改名为`waveshare35a.dtbo`。

2.修改`config.txt`文件，在最后加上`dtoverlay=waveshare35a`

3.修改`cmdline.txt`文件，在最后加上一个空格和`fbcon=map:10 fbcon=font:ProFont6x11 logo.nologo`

这样重启以后，经过一段时间的浅灰色的显示阶段，控制台就显示出来了。

这个办法目前在我的B+上的ArchlinuxARM上可用，uname -a显示为

```
Linux alarmpi 4.14.59-1-ARCH #1 SMP Tue Jul 31 00:57:25 UTC 2018 armv6l GNU/Linux
```
