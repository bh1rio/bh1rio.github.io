---
layout: post
title: 树莓派修改HDMI分辨率
date: 2018-07-04 07:54:22
categories: RaspberryPi
tags: 
---

收了一个HDMI的3.5寸屏，默认是1920的字太小看不清。修改启动分区中的config.txt文件，添加或者修改如下

```  
hdmi_group=2
hdmi_mode=87
hdmi_cvt 480 320 60 6 0 0 0
```
