---
title: "SPS门户首页的Web控件（1）"
date: 2004-11-10 15:30:00
layout: post
categories: SharePoint
tags: SharePoint
---

最近在忙着研究SPS，在定制首页的时候发现页面里用了大量的SPSWC的控件，提笔总结一下。这些好象都是MSDN里面没有的。

```xml
<SPSWC:CollaborationServerMetaTag>
```

这个标签将服务器上定制的<meta>标签写到页面。不需要页面中有HtmlForm的存在。

```xml
<SPSWC:ShowMessageToNonScriptableClients>
```

这个标签会在不支持脚本的浏览器上显示警示信息。不需要页面中有HtmlForm的存在。

```xml
<SPSWC:WebProperty>
```

这个标签会显示网站的属性例如：

```xml
<SPSWC:WebProperty Property=“SiteTitle“>
```

不需要页面中有HtmlForm的存在。

```xml
<SPSWC:CategoryProperty>
```

这个标签会显示子区域的属性例如：

```xml
<SPSWC:CategoryProperty Property=“Name“>
```

不需要页面中有HtmlForm的存在。

```xml
<SPSWC:CustomCSSResourceElement>
```

这个可以把定制的样式表写到标签的位置。不需要页面中有HtmlForm的存在。

```xml
<SPSWC:PageHeader>
```

这个标签可以输出设置里面设置的Logo。不需要页面中有HtmlForm的存在。

```xml
<SPSWC:CategoryNavigationWebPart>
```

这个标签可以输出子区域导航菜单。不需要页面中有HtmlForm的存在。