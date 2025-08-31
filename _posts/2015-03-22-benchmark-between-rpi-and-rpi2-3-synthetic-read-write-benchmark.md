---
layout: post
title: 树莓派1和树莓派2的性能对比（3）：Synthetic Read Write BenchMark
date: 2015-03-22 10:45:28
categories: 技术
tags: ARM LAMP Linux MySQL PHP RaspberryPi Apache
---
系列文章：  
  
[树莓派1和树莓派2的性能对比（1）：Synthetic PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-1-synthetic-php-benchmark.html)

[树莓派1和树莓派2的性能对比（2）：Synthetic MySQL BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-2-synthetic-mysql-benchmark.html)

上次树莓派1和Cubieboard对比的地址为：

[树莓派和Cubieboard对比测试(4) – Synthetic Read/Write BenchMark](http://just4fun.cn/?p=610)

|  | Pi | Pi2  
---|---|---  
PHP version | 5.6.6  
MySQL version | 5.5.5-10.0.17-MariaDB-log  
Server Software | Apache/2.4.12 (Unix) PHP/5.6.6  
Synthetic Read Write BenchMark  
test_1_create_dir | 0.0014 seconds | 0.0010 seconds  
test_2_create_tempfile | 0.0015 seconds | 0.0009 seconds  
test_3_write | 0.2340 seconds | 0.1246 seconds  
test_4_append | 0.1555 seconds | 0.0863 seconds  
test_4b_append | 0.1521 seconds | 0.0840 seconds  
test_5_fileinfo | 0.4854 seconds | 0.2825 seconds  
test_6_read_1024 | 4.3047 seconds | 1.2699 seconds  
test_6b_read_512 | 4.4377 seconds | 1.1854 seconds  
test_6c_read_256 | 6.0634 seconds | 1.7323 seconds  
test_6d_read_128 | 9.6558 seconds | 2.6062 seconds  
test_6e_read_64 | 14.4697 seconds | 4.5069 seconds  
test_6f_read_32 | 24.8038 seconds | 7.7512 seconds  
test_6g_read_16 | 52.2430 seconds | 15.5660 seconds  
test_7_read_8 | 74.0824 seconds | 21.8323 seconds  
test_9_readdir | 2.4713 seconds | 1.0116 seconds  
test_del_file | 0.0014 seconds | 0.0008 seconds  
test_del_tempdir | 0.0010 seconds | 0.0004 seconds  
Score(higher is better) | 124 | 413
