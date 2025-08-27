---
layout: post
title: 对于.net Framework的System.Net下面的CredentialCache类的补充说明
date: 2006-03-28 14:42:00
categories: AD aspnet dotnet
tags: dotnet AD aspnet
---

我在使用`CredentialCache`的`Add`方法的时候，不知道其他的几个`authType`怎么来写。在Google的帮助下，从微软的Support网站找到一些提示：

`Basic`：基本身份认证（明文传送用户名和密码）

`Digest`：Windows域服务器的摘要式身份认证

`Negotiate`：Windows集成身份认证（至少在这种认证方式下可用）

希望对调用有身份认证要求的WebService的朋友有帮助！
