---
layout: post
title: 树莓派1和树莓派2的性能对比（1）：Synthetic PHP BenchMark
date: 2015-03-22 10:37:34
categories: 技术
tags: ARM LAMP Linux MySQL PHP RaspberryPi Apache
---
两代树莓派硬件的主要区别是，主频高了一些，cpu变成了4核，ram变成了1GB。

上次树莓派1和Cubieboard对比的地址为：[树莓派和Cubieboard对比测试(2) – Synthetic PHP BenchMark](http://just4fun.cn/?p=608)

|     | Pi  | Pi2  |
| --- | --- | ---  |  
| PHP version | 5.6.6 ||
| MySQL version | 5.5.5-10.0.17-MariaDB-log || 
| Server Software | Apache/2.4.12 (Unix) PHP/5.6.6 ||  
| Synthetic PHP BenchMark |||  
| test_arithmetic | 0.2261 seconds | 0.1105 seconds  
| test_array_operators | 0.2856 seconds | 0.1700 seconds  
| test_bitwise | 0.0383 seconds | 0.0216 seconds  
| test_casting | 1.3268 seconds | 0.3272 seconds  
| test_chr_fixed | 1.8898 seconds | 0.5745 seconds  
| test_chr_hardcoded | 0.4025 seconds | 0.1578 seconds  
| test_chr_var | 1.8833 seconds | 0.5317 seconds  
| test_comment_loop | 0.1064 seconds | 0.0676 seconds  
| test_compare | 0.1038 seconds | 0.0417 seconds  
| test_compare_false | 0.0056 seconds | 0.0033 seconds  
| test_compare_invert | 0.0084 seconds | 0.0041 seconds  
| test_compare_strict | 0.0084 seconds | 0.0052 seconds  
| test_compare_unstrict | 0.0307 seconds | 0.0145 seconds  
| test_constants | 0.1514 seconds | 0.0500 seconds  
| test_crc32 | 0.1210 seconds | 0.0352 seconds  
| test_do_while | 0.4012 seconds | 0.2534 seconds  
| test_do_while_break | 0.0931 seconds | 0.0541 seconds  
| test_empty | 0.0057 seconds | 0.0038 seconds  
| test_empty_loop | 0.1062 seconds | 0.0676 seconds  
| test_foreach | 1.9737 seconds | 0.8063 seconds  
| test_get_class | 0.1385 seconds | 0.0381 seconds  
| test_global_scalar_assign | 0.0477 seconds | 0.0266 seconds  
| test_global_string_assign | 0.3587 seconds | 0.1446 seconds  
| test_if_constant | 0.0131 seconds | 0.0090 seconds  
| test_increment | 0.1622 seconds | 0.0494 seconds  
| test_is_array | 0.0365 seconds | 0.0123 seconds  
| test_is_object | 0.0396 seconds | 0.0124 seconds  
| test_is_type | 0.1358 seconds | 0.0442 seconds  
| test_isset | 0.0076 seconds | 0.0045 seconds  
| test_line | 0.0099 seconds | 0.0065 seconds  
| test_local_array_assign | 0.8565 seconds | 0.3604 seconds  
| test_local_boolean_assign | 0.0727 seconds | 0.0316 seconds  
| test_local_float_assign | 0.0731 seconds | 0.0319 seconds  
| test_local_hash_assign | 0.0685 seconds | 0.0314 seconds  
| test_local_integer_assign | 0.1053 seconds | 0.0319 seconds  
| test_local_object_assign | 0.0809 seconds | 0.0280 seconds  
| test_local_scalar_assign | 0.1006 seconds | 0.0448 seconds  
| test_local_string_assign | 0.2859 seconds | 0.1169 seconds  
| test_md5 | 0.1953 seconds | 0.0662 seconds  
| test_microtime | 0.6788 seconds | 0.2107 seconds  
| test_mt_rand | 0.0649 seconds | 0.0216 seconds  
| test_ord | 6.4353 seconds | 2.2288 seconds  
| test_ordered_functions | 1.0930 seconds | 0.4972 seconds  
| test_ordered_functions_references | 0.9427 seconds | 0.4826 seconds  
| test_preg_match | 0.4483 seconds | 0.1258 seconds  
| test_rand | 0.0735 seconds | 0.0223 seconds  
| test_references | 0.0108 seconds | 0.0072 seconds  
| test_sha1 | 0.2715 seconds | 0.0810 seconds  
| test_string_append | 0.2736 seconds | 0.0996 seconds  
| test_strlen | 0.0459 seconds | 0.0127 seconds  
| test_switch | 0.3535 seconds | 0.1650 seconds  
| test_time | 0.0618 seconds | 0.0256 seconds  
| test_unordered_functions | 1.1314 seconds | 0.5539 seconds  
| test_variable_variables | 0.1076 seconds | 0.0407 seconds  
| test_while | 0.4435 seconds | 0.2794 seconds  
| Score(higher is better) | 410 | 1082
