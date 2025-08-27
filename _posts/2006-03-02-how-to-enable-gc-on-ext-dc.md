---
layout: post
title: 额外的域控制器是否都可以升级为GC
date: 2006-03-02 14:20:00
categories: AD
tags: AD GC
---

问微软工程师的第二个问题“额外的域控制器是否都可以升级为GC”。

是的，所有域控制器都可以提升为GC。操作步骤如下：  

1. 在第一台DC上打开“Active Directory Sites and Services”  
2. 展开“Sites\Default-First-Site-Name\Servers\<第二台DC的名字>\NTDS Settings”  
3. 右键单击NTDS Settings，选择Properties  
4. 在General页面中，将“Global Catalog”前的勾勾上，点击OK。  
5. 重新启动第二台DC。
