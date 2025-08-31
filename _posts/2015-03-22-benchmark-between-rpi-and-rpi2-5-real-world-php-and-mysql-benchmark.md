---
layout: post
title: 树莓派1和树莓派2的性能对比（5）：Real World PHP &amp; MySQL BenchMark
date: 2015-03-22 10:51:26
categories: 技术
tags: ARM LAMP Linux MySQL PHP RaspberryPi Apache
---
系列文章：  
  
[树莓派1和树莓派2的性能对比（1）：Synthetic PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-1-synthetic-php-benchmark.html)

[树莓派1和树莓派2的性能对比（2）：Synthetic MySQL BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-2-synthetic-mysql-benchmark.html)

[树莓派1和树莓派2的性能对比（3）：Synthetic Read Write BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-3-synthetic-read-write-benchmark.html)

[树莓派1和树莓派2的性能对比（4）：Real World PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-4-real-world-php-benchmark.html)

上次树莓派1和Cubieboard对比的地址为:

[树莓派和Cubieboard对比测试(6) – Real World PHP & MySQL BenchMark](http://just4fun.cn/?p=612)

|  | Pi | Pi2  
|---|---|---  
PHP version | 5.6.6  
MySQL version | 5.5.5-10.0.17-MariaDB-log  
Server Software | Apache/2.4.12 (Unix) PHP/5.6.6  
Real World PHP & MySQL BenchMark  
test_page1a | 2.3365 seconds | 0.7525 seconds  
test_page1b | 2.3499 seconds | 0.7534 seconds  
test_page1c | 2.3339 seconds | 0.7531 seconds  
test_page1d | 2.3447 seconds | 0.7529 seconds  
test_page1e | 2.3353 seconds | 0.7529 seconds  
test_page2a | 6.4310 seconds | 1.8929 seconds  
test_page2b | 6.3900 seconds | 1.8923 seconds  
test_page2c | 6.4243 seconds | 1.8913 seconds  
test_page2d | 6.4153 seconds | 1.8927 seconds  
test_page2e | 6.4204 seconds | 1.8924 seconds  
test_page3a | 9.0395 seconds | 2.6444 seconds  
test_page3b | 9.3039 seconds | 2.6462 seconds  
test_page3c | 8.9621 seconds | 2.6440 seconds  
test_page3d | 8.9731 seconds | 2.6467 seconds  
test_page3e | 8.9627 seconds | 2.6429 seconds  
test_page4a | 12.5272 seconds | 3.7309 seconds  
test_page4b | 12.3040 seconds | 3.7344 seconds  
test_page4c | 12.7825 seconds | 3.7329 seconds  
test_page4d | 12.3229 seconds | 3.7370 seconds  
test_page4e | 12.4328 seconds | 3.7291 seconds  
Score(higher is better) | 198 | 665
