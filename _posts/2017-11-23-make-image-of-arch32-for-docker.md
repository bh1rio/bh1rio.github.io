---
layout: post
title: 制作Archlinux32的docker镜像(image)
date: 2017-11-23 02:53:18
categories: Docker Linux
tags: Archlinux Docker i686
---

docker hub里面的archlinux大部分是archlinux支持i686时期的镜像，目前archlinux不支持i686以后，这些镜像估计就不再支持i686了。我看了一些x86_64的镜像制作脚本，相当多的一部分都是直接用的其rootfs的tar来制作的，只有少数几种是直接从pacman获取包制作rootfs，挑了两种大牌的，如下：

1. 在Moby的github的捐献里，有一个archlinux的制作完整base包的脚本，我把获取包的mirror服务器改成了Archlinux32在日本的服务器以后，在i686的环境里面制作成功并运行了一个Archlinux32。我整理的脚本在<https://github.com/bh1rio/archlinux32-docker>
2. 另外一种方式是使用<https://github.com/archlinux/archlinux-docker> 的Makefile来直接用make的方式制作。这个不需要改Makefile，他是使用本机配置的mirror来获取包。惊喜是这个makefile可以制作rootfs。

对比两种方式，第二种方式的生成的包稍小，我怀疑有某些不必要的文件没有清理，不过还没有具体比较两个差异。

另，别问我为啥抱着i686玩docker：我给我的那个4盘位的小机器配好了Raid5,没理由扔到一边不管嘛
