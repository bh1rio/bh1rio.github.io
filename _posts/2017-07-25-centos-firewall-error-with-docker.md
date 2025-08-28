---
layout: post
title: CentOS的firewalld与docker有冲突
date: 2017-07-25 12:17:48
categories: Linux
tags: Docker
---

我这里表现为容器映射到宿主的端口，没有被防火墙保护。防火墙能用，但是报错，如下：

```
[root@localhost ~]# systemctl status firewalld  
● firewalld.service - firewalld - dynamic firewall daemon  
Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)  
Active: active (running) since 三 2017-07-26 00:42:31 CST; 7h left  
Docs: man:firewalld(1)  
Main PID: 760 (firewalld)  
Memory: 0B  
CGroup: /system.slice/firewalld.service  
└─760 /usr/bin/python -Es /usr/sbin/firewalld --nofork --nopid

7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t nat -C OUTPUT -m addrtype --dst-type LOCAL -j DOCKER ! --dst 127.0.0.0/8' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C FORWARD -o docker0 -j DOCKER' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C FORWARD -j DOCKER-ISOLATION' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t nat -C POSTROUTING -s 172.17.0.0/16 ! -o docker0 -j MASQUERADE' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t nat -C DOCKER -i docker0 -j RETURN' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -D FORWARD -i docker0 -o docker0 -j DROP' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C FORWARD -i docker0 -o docker0 -j ACCEPT' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C FORWARD -i docker0 ! -o docker0 -j ACCEPT' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C FORWARD -o docker0 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT' failed:  
7月 25 16:43:44 localhost.localdomain firewalld[760]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C FORWARD -o docker0 -j DOCKER' failed:
```
