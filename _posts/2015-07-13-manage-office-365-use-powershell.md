---
layout: post
title: 通过C#使用Powershell管理Office 365
date: 2015-07-13 10:46:18
categories: 技术
tags: Office365
---

这几天在做Office 365的管理Web Services，其中需要把一些使用Powershell管理Office 365的操作使用C#来完成。大体上的操作都能完成但是有细节。

1. 设置用户属性，设置用户授权。

可以参考这个微软的这个例子：https://code.msdn.microsoft.com/office/Office-365-Manage-licenses-fb2c6413

需要注意的是：

1)Powershell本版也高于3.0。当前版本是4.0。

2)需要为Powershell安装MS在线服务登录助手和Azure AD的模块。
  
3)如果在64位系统上安装了64位的MS登录助手的话，需要将

`MSOnline` 和 `MSOnline Extended` 两个文件夹从 `C:\Windows\System32\WindowsPowerShell\v1.0\Modules\`
拷贝到 `C:\Windows\SysWOW64\WindowsPowerShell\v1.0\Modules\`

第三个是一个安装包的问题。在64位系统中，是同时包含32位和64位Powershell的，默认启动的Powershell是32位的，登录助手默认安装到32位的模块库中，64位的模块库中没有。当我们用命令行检测的时候，没有任何问题，当我们通过C#来调用的时候，就会采用64位的Powershell来执行，这个时候就会报缺少模块引用造成的命令无法找到的错误。解决办法也很简单，就像上面说的，复制到64位Powershell的模块库就好了。

4)如果是世纪互联的话，最后在设置授权之前，先获取授权列表。因为墙外的Office365的授权因为国内法律的问题，会和世纪互联提供的授权有区别，所以授权的字样也会有变化。

2. 启用Exchange Online的邮箱

可以参开这个微软转发的MVP写的例子：http://blogs.msdn.com/b/mvpawardprogram/archive/2011/08/29/mvps-for-exchange-online-calling-exchange-online-powershell-cmdlets-from-c.aspx

需要注意的是：

1)世纪互联用户不能再使用 https://ps.outlook.com/powershell 获取远程对话了，需要使用 https://partner.outlook.cn/powershell-liveid

2)如果是一个单一授权的Office365订阅，新账号会默认选择这个单一的授权，只有在有多重授权混合的时候，创建账号的时候才会有选项。

3)单一授权的时候，在分配授权以后，会自动创建授权相应的邮箱账号。所以这个时候不需要单独开启邮箱，直接分配授权就好。

3. 因为Office 365是一个在线服务，以上的内容只在当前时间确定是没有问题的。
