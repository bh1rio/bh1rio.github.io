---
title: "说说Yet Another Forum的域整合验证"
date: 2004-11-05 15:28:00
layout: post
categories: aspnet
tags: aspnet
---

上次向飞鹰推荐了Yet Another Forum论坛，但是飞鹰没有用。他不用没关系，我用。我在现在实施SPS的项目中，客户不满意SPS的讨论版。我本来想使用ASP.NET Forum 2，但是现在发现她变成商业的了，于是我们决定使用Yet Another Forum，它是GPL的。开源+免费有什么不好？

YetAnotherForum的域整合非常简单，首先要在安装一个非域验证的实例，在选择管理员账号的时候比较有技巧：帐号最好和将来域里面准备作为论坛管理员的账号一致。这样做是为了在与域整合以后不用再调整论坛的管理员了。其他的安装可以按照软件包里面的说明进行。

在非域验证配置完成以后，我们开始进行域整合的配置。我们需要修改Web.Config，将验证方式改为

```xml
<authentication mode="Windows">
</authentication>
```

然后修改IIS关于这个应用的验证方式为Windows域服务器的摘要式身份验证，同时将你论坛程序所在的目录赋予读/执行/列表权限给相应的域用户。

这样在你再次访问的时候，你就会发现已经能像SPS一样整合使用与账号了。而你当初指定的那个账号会自动变成管理员了。这样你就可以开始你的其他论坛配置了。