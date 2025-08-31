---
layout: post
title: 树莓派1和树莓派2的性能对比（2）：Synthetic MySQL BenchMark
date: 2015-03-22 10:41:08
categories: 技术
tags: ARM LAMP Linux MySQL PHP RaspberryPi Apache
---
系列文章：  
  
[树莓派1和树莓派2的性能对比（1）：Synthetic PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-1-synthetic-php-benchmark.html)

上次树莓派1和Cubieboard对比的地址为：

[树莓派和Cubieboard对比测试(3) – Synthetic MySQL BenchMark](http://just4fun.cn/?p=609)

|  | Pi | Pi2  
---|---|---  
PHP version | 5.6.6  
MySQL version | 5.5.5-10.0.17-MariaDB-log  
Server Software | Apache/2.4.12 (Unix) PHP/5.6.6  
Synthetic MySQL BenchMark  
test_db_setup | 1.3504 seconds | 0.4811 seconds  
test_distinctcolumn | 6.0972 seconds | 2.0539 seconds  
test_fetcharray | 3.4702 seconds | 1.0954 seconds  
test_fetchassoc | 3.1557 seconds | 1.0263 seconds  
test_fetchlength | 3.1741 seconds | 1.0148 seconds  
test_fetchrow | 3.1540 seconds | 1.2152 seconds  
test_fieldflags | 13.0071 seconds | 3.5117 seconds  
test_maxget | 2.8478 seconds | 0.8929 seconds  
test_numfields | 8.9720 seconds | 2.2549 seconds  
test_numrows | 10.1692 seconds | 2.2571 seconds  
test_rowcount | 1.0088 seconds | 0.2399 seconds  
test_sort | 15.3296 seconds | 4.1467 seconds  
test_sort2 | 16.1388 seconds | 4.1016 seconds  
test_sort3 | 15.2947 seconds | 4.1456 seconds  
test_sumcolumn | 2.8440 seconds | 0.9381 seconds  
test_write | 1.3475 seconds | 0.3367 seconds  
test_write2 | 1.3922 seconds | 0.3848 seconds  
test_write3 | 1.4473 seconds | 0.3876 seconds  
test_write_cleanup | 0.0107 seconds | 0.0044 seconds  
Score(higher is better) | 145 | 524
