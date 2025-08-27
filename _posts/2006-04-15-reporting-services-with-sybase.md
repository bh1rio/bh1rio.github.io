---
layout: post
title: 也说报表服务遇见了Sybase
date: 2006-04-15 15:16:00
categories: SQLServer
tags: ReportingServices SQLServer Sybase
---

[ccBoy遇见的问题](http://www.dotnettools.org/Blog/article.asp?id=117)，在我客户这里也有，但是客户似乎没有把这当作一个问题。我在客户这里部署的ReportingService还是SQLServer2000里面的，不过情景应该类似。客户也是将Sybase里面行以千万计的数据导出到SQLServer2000当中，原因一方面是怕报表的查询影响业务数据库中实时数据的插入，一方面是因为在ReportingService对Sybase数据库使用参数的时候报错。联想到在ASP.NET当中使用Sybase数据库的时候，Sybase的ODBC驱动不支持SQL当中使用参数，窃估计是ODBC驱动的硬伤...曾经想找一个Sybase的.NET的连接器，但是总没有找到。

客户导数据的耐心还是值得称道的，在SQLServer2000中的数据转换服务中，DTS包达到了7个，最大的一个DTS包中导了二十多个表，导数据的流程达到了四十多步！每天大概从4个不同的系统中倒入大概4千万行左右的数据，同时还要将数据关联汇总。那个SQLServer2000的数据库基本上过了晚上12点就开始忙，大概要忙8个小时左右...

ccBoy的问题我不知什么自动的方法来解决，对SQLServer2005还不熟。但是他提到SSIS的问题应该是在SQLServer2000当中就存在了...

> 2025-08-27 注: ccBoy的网站已经不能访问了。