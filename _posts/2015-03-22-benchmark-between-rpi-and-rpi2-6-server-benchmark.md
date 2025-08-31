---
layout: post
title: 树莓派1和树莓派2的性能对比（6）：Server Benchmark
date: 2015-03-22 10:58:20
categories: 技术
tags: ARM LAMP Linux MySQL PHP RaspberryPi Apache Box
---
系列文章：  
  
[树莓派1和树莓派2的性能对比（1）：Synthetic PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-1-synthetic-php-benchmark.html)

[树莓派1和树莓派2的性能对比（2）：Synthetic MySQL BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-2-synthetic-mysql-benchmark.html)

[树莓派1和树莓派2的性能对比（3）：Synthetic Read Write BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-3-synthetic-read-write-benchmark.html)

[树莓派1和树莓派2的性能对比（4）：Real World PHP BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-4-real-world-php-benchmark.html)

[树莓派1和树莓派2的性能对比（5）：Real World PHP & MySQL BenchMark](http://just4fun.cn/2015/03/22/benchmark-between-rpi-and-rpi2-5-real-world-php-and-mysql-benchmark.html)

上次树莓派1和Cubieboard对比的地址为:

[树莓派和Cubieboard对比测试(7) – Server Benchmark](http://just4fun.cn/?p=613)

|  | Pi | Pi2  |
|---|---|---|  
PHP version | 5.6.6  
MySQL version | 5.5.5-10.0.17-MariaDB-log  
Server Software | Apache/2.4.12 (Unix) PHP/5.6.6  
Server Benchmark  
test_1_create_dir | 0.0017 seconds | 0.0009 seconds  
test_1_small_page | 0.4914 seconds | 0.1713 seconds  
test_1b_small_page | 0.4885 seconds | 0.1394 seconds  
test_1c_small_page | 0.4882 seconds | 0.1392 seconds  
test_1d_small_page | 0.4898 seconds | 0.1392 seconds  
test_1e_small_page | 0.4889 seconds | 0.1397 seconds  
test_2_create_tempfile | 0.0016 seconds | 0.0008 seconds  
test_2_medium_page | 1.3283 seconds | 0.4323 seconds  
test_2b_medium_page | 1.3281 seconds | 0.4348 seconds  
test_2c_medium_page | 1.3297 seconds | 0.4374 seconds  
test_2d_medium_page | 1.3283 seconds | 0.4361 seconds  
test_2e_medium_page | 1.3318 seconds | 0.4373 seconds  
test_3_large_page | 3.9221 seconds | 1.3041 seconds  
test_3_write | 0.1565 seconds | 0.0558 seconds  
test_3b_large_page | 3.9231 seconds | 1.3027 seconds  
test_3c_large_page | 3.9270 seconds | 1.3016 seconds  
test_3d_large_page | 3.9473 seconds | 1.3015 seconds  
test_3e_large_page | 3.9296 seconds | 1.3024 seconds  
test_4_append | 0.1028 seconds | 0.0383 seconds  
test_4_huge_page | 6.2111 seconds | 2.0126 seconds  
test_4b_append | 0.0999 seconds | 0.0376 seconds  
test_4b_huge_page | 6.1738 seconds | 2.0134 seconds  
test_4c_huge_page | 6.2370 seconds | 2.0141 seconds  
test_4d_huge_page | 6.2073 seconds | 2.0137 seconds  
test_4e_huge_page | 6.2364 seconds | 2.0114 seconds  
test_5_fileinfo | 0.3223 seconds | 0.1466 seconds  
test_6_read_1024 | 1.9919 seconds | 0.5921 seconds  
test_6b_read_512 | 1.9095 seconds | 0.5338 seconds  
test_6c_read_256 | 2.5433 seconds | 0.7696 seconds  
test_6d_read_128 | 4.1118 seconds | 1.1324 seconds  
test_6e_read_64 | 7.1683 seconds | 2.0073 seconds  
test_6f_read_32 | 12.9881 seconds | 3.5275 seconds  
test_6g_read_16 | 28.5116 seconds | 7.2687 seconds  
test_7_read_8 | 33.9870 seconds | 9.7546 seconds  
test_9_readdir | 1.6711 seconds | 0.6747 seconds  
test_arithmetic | 0.0060 seconds | 0.0015 seconds  
test_array_operators | 0.0101 seconds | 0.0028 seconds  
test_bitwise | 0.0013 seconds | 0.0005 seconds  
test_casting | 0.0283 seconds | 0.0066 seconds  
test_chr_fixed | 0.0482 seconds | 0.0116 seconds  
test_chr_hardcoded | 0.0093 seconds | 0.0032 seconds  
test_chr_var | 0.0407 seconds | 0.0107 seconds  
test_comment_loop | 0.0022 seconds | 0.0014 seconds  
test_compare | 0.0020 seconds | 0.0009 seconds  
test_compare_false | 0.0002 seconds | 0.0001 seconds  
test_compare_invert | 0.0003 seconds | 0.0001 seconds  
test_compare_strict | 0.0004 seconds | 0.0001 seconds  
test_compare_unstrict | 0.0008 seconds | 0.0003 seconds  
test_connect_db | 0.0587 seconds | 0.0172 seconds  
test_constants | 0.0039 seconds | 0.0011 seconds  
test_crc32 | 0.0027 seconds | 0.0007 seconds  
test_db_setup | 0.6793 seconds | 0.1770 seconds  
test_del_file | 0.0014 seconds | 0.0008 seconds  
test_del_tempdir | 0.0010 seconds | 0.0004 seconds  
test_distinctcolumn | 1.8773 seconds | 0.6269 seconds  
test_do_while | 0.0097 seconds | 0.0051 seconds  
test_do_while_break | 0.0021 seconds | 0.0011 seconds  
test_empty | 0.0003 seconds | 0.0001 seconds  
test_empty_loop | 0.0024 seconds | 0.0014 seconds  
test_fetcharray | 1.3069 seconds | 0.4140 seconds  
test_fetchassoc | 1.1749 seconds | 0.3709 seconds  
test_fetchlength | 1.1717 seconds | 0.3643 seconds  
test_fetchrow | 1.1665 seconds | 0.3681 seconds  
test_fieldflags | 3.4805 seconds | 1.0895 seconds  
test_foreach | 0.0433 seconds | 0.0153 seconds  
test_get_class | 0.0030 seconds | 0.0008 seconds  
test_global_scalar_assign | 0.0014 seconds | 0.0006 seconds  
test_global_string_assign | 0.0077 seconds | 0.0029 seconds  
test_if_constant | 0.0004 seconds | 0.0002 seconds  
test_increment | 0.0029 seconds | 0.0010 seconds  
test_is_array | 0.0010 seconds | 0.0003 seconds  
test_is_object | 0.0010 seconds | 0.0003 seconds  
test_is_type | 0.0032 seconds | 0.0009 seconds  
test_isset | 0.0003 seconds | 0.0001 seconds  
test_line | 0.0004 seconds | 0.0002 seconds  
test_local_array_assign | 0.0342 seconds | 0.0096 seconds  
test_local_boolean_assign | 0.0021 seconds | 0.0007 seconds  
test_local_float_assign | 0.0021 seconds | 0.0007 seconds  
test_local_hash_assign | 0.0019 seconds | 0.0007 seconds  
test_local_integer_assign | 0.0020 seconds | 0.0007 seconds  
test_local_object_assign | 0.0020 seconds | 0.0006 seconds  
test_local_scalar_assign | 0.0031 seconds | 0.0010 seconds  
test_local_string_assign | 0.0078 seconds | 0.0025 seconds  
test_maxget | 0.9734 seconds | 0.3113 seconds  
test_md5 | 0.0040 seconds | 0.0014 seconds  
test_microtime | 0.0163 seconds | 0.0043 seconds  
test_mt_rand | 0.0016 seconds | 0.0005 seconds  
test_numfields | 2.5441 seconds | 0.7369 seconds  
test_numrows | 2.5617 seconds | 0.7237 seconds  
test_ord | 0.1501 seconds | 0.0443 seconds  
test_ordered_functions | 0.0234 seconds | 0.0101 seconds  
test_ordered_functions_references | 0.0228 seconds | 0.0098 seconds  
test_page1a | 0.2641 seconds | 0.0792 seconds  
test_page1b | 0.2585 seconds | 0.0781 seconds  
test_page1c | 0.2621 seconds | 0.0779 seconds  
test_page1d | 0.2613 seconds | 0.0781 seconds  
test_page1e | 0.2598 seconds | 0.0781 seconds  
test_page2a | 0.7814 seconds | 0.2352 seconds  
test_page2b | 0.7866 seconds | 0.2332 seconds  
test_page2c | 0.8034 seconds | 0.2333 seconds  
test_page2d | 0.7826 seconds | 0.2341 seconds  
test_page2e | 0.7810 seconds | 0.2342 seconds  
test_page3a | 1.1535 seconds | 0.3559 seconds  
test_page3b | 1.1828 seconds | 0.3559 seconds  
test_page3c | 1.1847 seconds | 0.3560 seconds  
test_page3d | 1.1614 seconds | 0.3560 seconds  
test_page3e | 1.1867 seconds | 0.3562 seconds  
test_page4a | 1.5888 seconds | 0.4892 seconds  
test_page4b | 1.5672 seconds | 0.4886 seconds  
test_page4c | 1.5672 seconds | 0.4895 seconds  
test_page4d | 1.5980 seconds | 0.4899 seconds  
test_page4e | 1.5838 seconds | 0.4891 seconds  
test_preg_match | 0.0111 seconds | 0.0028 seconds  
test_rand | 0.0015 seconds | 0.0005 seconds  
test_references | 0.0004 seconds | 0.0002 seconds  
test_rowcount | 0.5033 seconds | 0.1234 seconds  
test_sha1 | 0.0073 seconds | 0.0016 seconds  
test_sort | 4.1689 seconds | 1.2160 seconds  
test_sort2 | 4.1101 seconds | 1.3251 seconds  
test_sort3 | 4.2083 seconds | 1.2172 seconds  
test_string_append | 0.0058 seconds | 0.0021 seconds  
test_strlen | 0.0010 seconds | 0.0003 seconds  
test_sumcolumn | 1.0162 seconds | 0.3223 seconds  
test_switch | 0.0070 seconds | 0.0034 seconds  
test_time | 0.0016 seconds | 0.0005 seconds  
test_unordered_functions | 0.0266 seconds | 0.0112 seconds  
test_variable_variables | 0.0032 seconds | 0.0009 seconds  
test_while | 0.0091 seconds | 0.0056 seconds  
test_write | 0.6625 seconds | 0.1705 seconds  
test_write2 | 0.7029 seconds | 0.1888 seconds  
test_write3 | 0.7162 seconds | 0.1961 seconds  
test_write_cleanup | 0.0103 seconds | 0.0040 seconds  
Score(higher is better) | 144 | 484
