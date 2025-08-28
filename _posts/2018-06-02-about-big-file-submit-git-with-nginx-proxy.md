---
layout: post
title: 关于通过https提交git内容过大
date: 2018-06-02 08:54:17
categories: Git
tags: Git
---

这个问题是给gogs前面加了nginx起https发生的，报错如下：

```
error: RPC failed; HTTP 413 curl 22 The requested URL returned error: 413 Request Entity Too Large  
```

用 https://stackoverflow.com/questions/7489813/github-push-error-rpc-failed-result-22-http-code-413 的办法添加 `client_max_body_size 50m;`解决。

> 注：
>
> 1. 以前没给gitlab前置nginx起https，但是这个只设置nginx就解决问题，估计是nginx的问题。
> 2. `client_max_body_size`默认1m
> 3. `client_max_body_size`可以加载server或者http内，建议加在server内，减少影响范围。
> 4. 大小根据自己的设置。
