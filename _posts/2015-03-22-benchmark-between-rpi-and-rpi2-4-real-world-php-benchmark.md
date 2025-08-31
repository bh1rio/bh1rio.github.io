---
layout: post
title: 树莓派1和树莓派2的性能对比（4）：Real World PHP BenchMark
date: 2015-03-22 10:48:17
categories: 技术
tags: ARM LAMP Linux MySQL PHP RaspberryPi Apache
---
系列文章：  
  
[树莓派1和树莓派2的性能对比（1）：Synthetic PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-1-synthetic-php-benchmark.html)

[树莓派1和树莓派2的性能对比（2）：Synthetic MySQL BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-2-synthetic-mysql-benchmark.html)

[树莓派1和树莓派2的性能对比（3）：Synthetic Read Write BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-3-synthetic-read-write-benchmark.html)

上次树莓派1和Cubieboard对比的地址为：

[树莓派和Cubieboard对比测试(5) – Real World PHP BenchMark](http://just4fun.cn/?p=611)

|  | Pi | Pi2  
---|---|---  
PHP version | 5.6.6  
MySQL version | 5.5.5-10.0.17-MariaDB-log  
Server Software | Apache/2.4.12 (Unix) PHP/5.6.6  
Real World PHP BenchMark  
test_1_small_page | 1.1907 seconds | 0.5099 seconds  
test_1b_small_page | 1.1620 seconds | 0.3424 seconds  
test_1c_small_page | 1.1608 seconds | 0.3422 seconds  
test_1d_small_page | 1.1648 seconds | 0.3435 seconds  
test_1e_small_page | 1.1701 seconds | 0.3411 seconds  
test_2_medium_page | 3.2147 seconds | 1.0279 seconds  
test_2b_medium_page | 3.2330 seconds | 1.0329 seconds  
test_2c_medium_page | 3.3178 seconds | 1.0358 seconds  
test_2d_medium_page | 3.3654 seconds | 1.0369 seconds  
test_2e_medium_page | 3.3518 seconds | 1.0372 seconds  
test_3_large_page | 9.9856 seconds | 3.1942 seconds  
test_3b_large_page | 10.2158 seconds | 3.1947 seconds  
test_3c_large_page | 9.9806 seconds | 3.1957 seconds  
test_3d_large_page | 10.2136 seconds | 3.1958 seconds  
test_3e_large_page | 10.2217 seconds | 3.1928 seconds  
test_4_huge_page | 15.8610 seconds | 4.9444 seconds  
test_4b_huge_page | 15.5103 seconds | 4.9461 seconds  
test_4c_huge_page | 15.8390 seconds | 4.9671 seconds  
test_4d_huge_page | 15.6031 seconds | 4.9714 seconds  
test_4e_huge_page | 15.6240 seconds | 4.9754 seconds  
Score(higher is better) | 297 | 941
