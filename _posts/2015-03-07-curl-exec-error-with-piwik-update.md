---
layout: post
title: Piwik升级，提示curl_exec超时问题解决
date: 2015-03-07 08:13:30
categories: 技术
tags: Piwik
---

如果你的Piwik升级的时候提示curl_exec出错的话，恭喜你，估计你是在2.11.0或2.11.1这两个版本。2.11.0默认是10秒，2.11.1默认是30秒。如果这个时间搞不定，就报错。估计没谁的主机能这么快，比如我的。

查了一下，可以修改`plugins/CoreUpdater/Controller.php`的175行。

如果你是2.11.0，应该是如下的样子

```php
Http::fetchRemoteFile($url, $this->pathPiwikZip);
```
如果你是2.11.1，应该是如下的样子

```php
Http::fetchRemoteFile($url, $this->pathPiwikZip, 0, 30);
```

2.11.2以后的样子：

```php
Http::fetchRemoteFile($url, $this->pathPiwikZip, 0, 120);
```

修改版本很简单，修改为2.11.2的样子就好，因为2.11.2就没有这个问题了。
