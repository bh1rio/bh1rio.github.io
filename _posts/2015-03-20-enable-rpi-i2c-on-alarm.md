---
layout: post
title: 启用Raspberry树莓派的i2c总线
date: 2015-03-20 02:13:11
categories: 技术
tags: Archlinux I2C IoT Linux RaspberryPi ARM Box
---

其实我是在看mono的i2c接口程序，发现我的/dev里面没有i2c-0和i2c-1这两个设备，于是查了一下。发现按照国内大部分教程为linux添加i2c-dev的驱动以后，并没有解决问题。翻墙找了找，如果单纯添加驱动不能解决问题的话，就需要修改/boot/config.txt了。

修改`/boot/config.txt`方法：

找到 `device_tree_param=i2c_arm=on` 和 `device_tree_param=i2c_vc=on` ，然后将其前面的注释去掉。

树莓派应该是有两条i2c总线？我不确定。不过一般情况在，/dev中会有`i2c-0`和`i2c-1`两个设备，上面两条如果只取消注释一条的话，那么只会出现一个i2c设备。`i2c_arm`对应的是`i2c-1`，`i2c_vc`对应的是`i2c-0`。

修改`/etc/modules-load.d/raspberrypi.conf`方法：

最后面添加`i2c-dev`。

这时候重启应该就可以看到/dev里面的i2c设备了。

再往下可以安装i2c-tools来查看工作状态了。这个自行搜索怎么用吧，我也没研究呢。

题外话：

* 从上面的试验可以看出，config.txt的优先级要比linux内核驱动的优先级高，可以直接关闭设别，这样驱动也就无效了。
* config.txt里面有i2c的速率设置方式，相应模块也有速率设置的方式，这两个优先级没有测试。
* 有的linux发布上还有blacklist的设置，还需要从黑名单中去掉i2c设备。ArchLinuxARM这个是空的。
* 目前是在Pi 1 B+上进行的测试。在Pi 1 B和Pi 2 B上还没有测试。根据文档看，貌似有区别，但是中说纷纭，有待测试。
* DS1307硬时钟是i2c接口的，所以在使用DS1307前，需要保证i2c正常。
