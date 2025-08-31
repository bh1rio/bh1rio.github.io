---
layout: post
title: SharePoint 2013中PerformancePoint仪表板设计器连接Analysis Services 2012的问题
date: 2014-10-11 02:05:19
categories: 技术
tags: SharePoint SQLServer PerformancePoint
---

在SharePoint 2013的PerformancePoint仪表板设计器在创建链接到AnalysisServices 2012的数据链接的时候，数据库列表无法获取服务器上的数据库。这个问题挺让人困惑的。翻墙查询，发现有老外对问题作了分析，还提出了解决办法。

“[Why can’t SharePoint Dashboard Designer 2013 connect to SQL Analysis Services 2012?](http://www.chrismcnulty.net/blog/Lists/Posts/Post.aspx?ID=74)”里面找到是ADOMD的版本过新导致的问题，并给出了老版版的ADOMD的下载地址：http://www.microsoft.com/en-us/download/details.aspx?id=16978 。

之后的一篇“[PerformancePoint Dashboard Designer Can’t Find Any SSAS Databases or Cubes Part II](http://www.chrismcnulty.net/blog/Lists/Posts/Post.aspx?ID=135)”给出了不安装老版本ADOMD的方法：修改`C:\Program Files\Microsoft Office Servers\15.0\WebServices\PpsMonitoringServer`中的Web.Config文件。在这个文件中找到如下这段：  

```xml
<runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.AnalysisServices.AdomdClient" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="9.0.0.0" newVersion="10.0.0.0" />  
        </dependentAssembly>  
    </assemblyBinding>  
</runtime>
```

将其中的

```
oldVersion="9.0.0.0" newVersion="10.0.0.0"
```

修改为

```
OldVersion="10.0.0.0" newVersion="11.0.0.0"
```

然后重启IIS。

这个方法使得PerformancePoint可以使用最新版的ADOMD，也就不用再装老版本的ADOMD了。
