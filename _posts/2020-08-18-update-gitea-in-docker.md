---
layout: post
title: 关于通过Docker部署的gitea的升级
date: 2020-08-18 07:43:44
categories: Docker
tags: Git
---

最早以前用gitlab，但是太耗资源了。换了gogs，发现总不更新。最后换了gitea。

之前放在托管服务器上的是使用docker部署的gitea 1.6.1版，好长时间没升级了，这次升级了一下，升级到了当前最新的1.12.3版。

按照gitea官方文档，原来的docker容器删掉换新的docker容器就好了，但是前提是容器的/data必须映射到了宿主。也就是说，docker容器删掉，数据不会丢失。

我升级的时候也没有一步到位，先是升级到1.8.3，再升级到1.12.3。避免跨度太大，扯到……docker。

现在升级完看上去都正常。另外，升级前记得备份映射到宿主的/data。
