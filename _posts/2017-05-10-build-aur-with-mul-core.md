---
layout: post
title: 使用多处理器编译AUR
date: 2017-05-10 06:16:20
categories: Linux
tags: Archlinux
---

archlinux用aur编译的时候，根据top看，多处理器没有用起来，于是研究了一下，发现可以修改/etc/makepkg.conf来修改make的环境变量，启用多处理。具体如下：

去掉MAKEFLAGS前面的注释，并根据处理器数量修改-j后面数据，双核为-j2，四核为-j4

```  
MAKEFLAGS="-j2"
```

这个提升还是比较明显的。
