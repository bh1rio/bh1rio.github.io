---
layout: post
title: 为SpringBoot做了一个Docker的Dockerfile
date: 2017-07-25 12:08:17
categories: 未分类
tags: Docker
---

话不多说，帖文件：

```dockerfile
FROM java:openjdk-8u111-jdk
VOLUME /tmp
ADD springboot.jar app.jar
ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -jar /app.jar" ]
```
