---
layout: post
title: Office Web Apps升级
date: 2014-10-20 10:53:46
categories: 技术
tags: SharePoint
---

这两天新做了一个SharePoint的开发环境，当中有一个OWA的服务器，直接连上Windows Updates一顿狂升级，然后就用不了。

找到了半天的错误信息，然后翻墙找问题，结果问题居然是OWA每升级一次，就要重新创建OWA的Farm。

不吐槽了，开始重建：

首先退场：

```powershell  
Remove-OfficeWebAppsMachine
```

然后重新建场，其实和第一次创建是一样的：

```powershell
New-OfficeWebAppsFarm -InternalURL "http://Contoso-WAC" -AllowHttp -EditingEnabled
```

