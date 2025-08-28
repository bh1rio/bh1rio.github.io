---
layout: post
title: 在Docker里面运行MS SQLServer 2017的Linux版本
date: 2017-11-16 06:50:40
categories: Docker Linux SQLServer
tags: Docker Linux SQLServer
---

今天看见Docker的Hub里面的microsoft/mssql-server-linux已经升级到了2017-CU1，就顺手装了一个。可以用如下命令：

```bash
docker run --name mssql -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=' -e 'MSSQL_PID=Standard' -p 1433:1433 -d microsoft/mssql-server-linux:2017-CU1</yourstrong!passw0rd>
```

其中有意思的是MSSQL_PID这个参数，PID是Product ID (PID)或者版本的意思，可以送的参数包括：

* Developer :开发版，默认值  
* Express :这个不用说了  
* Standard :标准版  
* Enterprise :企业版  
* EnterpriseCore :这个你们自己试试吧

![01448D53](/images/2017/11/01448D53.png)赶快搞起来吧
