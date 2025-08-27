---
layout: post
title: SPS的安全机制与ASP.NET的安全机制还是有区别的
date: 2006-01-13 13:36:00
categories: AD SharePoint
tags: AD SharePoint
---
这几天一直写一个在SPS当中修改AD用户密码的Webpart。我向鞠海洋大哥要来了他写的代码，仔细研究了，自己也动手写了一个。但是包括鞠大哥写的和我写的都不用正确运行，总是捕捉到异常信息。不同的是，鞠大哥的代码可以显示用户的displayName属性，而我的显示不了。

昨天就想起来在ASP.NET中测试一下吧，毕竟ASP.NET当中条是要容易些。我有在写Webpart之前，先用ASP.NET预演的习惯。但是却发现ASP.NET当中不仅可以显示displayName属性，连密码也可以修改了。于是又仔细看了鞠大哥的代码，发现他并不是从AD用户的displayName属性显示的用户名称，而是通过SPS的CurrentUser对象来获取的用户名称。这样在仔细测试后可以发现，在SPS的Webpart当中是没有办法读取AD内数据的，即使将SPS网站的安全信任级别提高到了“Full”也是不行的。

详细的错误信息：  

```
System.Runtime.InteropServices.COMException (0x80070035): 找不到网络路径。 
at System.DirectoryServices.DirectoryEntry.Bind(Boolean throwIfFail) 
at System.DirectoryServices.DirectoryEntry.Bind() 
at System.DirectoryServices.DirectoryEntry.get_NativeObject() 
at System.DirectoryServices.DirectoryEntry.Invoke(String methodName, Object[] args) 
at nChi.WebParts.Utility.UserCtrl.chgPwd()
```  
以此猜测这可能是SPS把有关的COM调用给屏蔽到了...
