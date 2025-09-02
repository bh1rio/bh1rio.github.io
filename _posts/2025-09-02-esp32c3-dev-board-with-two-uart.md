---
title: "一个有意思的ESP32C3开发板"
date: 2025-09-02 20:14:00 8000
layout: post
categories: 技术
tags: esp32 micropython
---

从闲鱼买了一块开源的ESP32C3开发板，很有意思。

闲鱼地址就不给大家写了，留个开源的地址：https://oshwhub.com/wanfang/esp32c3。

![](/images/2025/09/2025-09-02_01.jpg)

到手我就先刷了个helloworld试机，没问题就确认收货了。但是刷上micropython以后，thonny不认设备。和这板子的开发者沟通反复测试，最后他问我你要不反插试试。这时我才知道正插和反插效果不一样。反插上去，发现/dev/ttyUSB0没了，我还以为反插坏了，他提醒我才发现反插是设备/dev/ttyACM0。

这下我的兴趣来了，本来买这个板子是因为这个板子和LCD屏可以在面包板上直插免连线，可是这个有意思的双串口是额外的惊喜。

先说背景，ESP32C3的18和19引脚可以直接作为USB的CDC设备，连接电脑会出现一个免驱的串口，在Linux上为ttyACMx设备。还有若干UART设备，如这个板子使用ch340连接电脑也会有一个串口设备。Win10/11上这个串口可以通过Windows Update安装驱动，Linux内核内置ch34x系列的驱动，Linux上设备名为ttyUSBx。ttyACMx和ttyUSBx的x是按顺序分配的数字，第一个是0。除了ESP32C3以外，ESP32S3等新的芯片，都带这个USB CDC设备。一般的ESP32C3或者ESP32S3的开发板，或是选择ch34x系列芯片，或是省掉这个ch34x，但是没有同时支持这两种串口的。

首先我实验了helloworld用两个串口刷机，以及分别监视串口的log输出。然后又刷了当前最新的micropython 1.26.0来测试。结论如下：

1. 两种串口的刷机效果一样。无论是helloworld还是micropython。
2. helloworld的输出是一样的，但是ttyACM0的输出有错误信息，看上去是来源于启动后第一阶段的bootloader，第二阶段都是一样的没有错误。估计需要啥设置，但是我还不清楚具体需要什么设置。前面的这图是ttyUSB0的，后面是ttyACM0的。

![](/images/2025/09/2025-09-02_02.jpg)

![](/images/2025/09/2025-09-02_03.jpg)

3. micorpython在两个串口上都能启用repl。但是thonny只能连接ttyACM0这个。下图是使用idf_monitor工具连接micrpython repl的截图。

![](/images//2025/09//2025-09-02_04.png)

因为micropython除了使用串口做repl交互以外，还使用串口做文件传输等等其他功能，我估计可能是micropython并不支持在所有的串口上同时做这些操作，导致thonny只能连ttyACM0。至于能不能通过自己编译micropython应该能切换这个串口，目前我还不确定。