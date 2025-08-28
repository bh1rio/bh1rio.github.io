---
layout: post
title: 在Archlinux中使用swapfile
date: 2018-02-27 15:36:16
categories: Linux
tags: Linux
---

swapfile简单的说就是不使用交换分区而使用文件来交换内存，这个有点像windows的pagefile。我为什么要使用swapfile而不使用交换分区呢？因为我有强迫症，我总是迫切自己roofs一定要在sda1上……

步骤比较简单:

1. 创建交换文件

```bash  
fallocate -l 512M /swapfile
```

需要注意的是，如果文件系统是XFS的话，这么做可能会导致问题，那么可以用dd来完成：

```bash  
dd if=/dev/zero of=/swapfile bs=1M count=512
```

2. 修改文件的权限

```bash  
chmod 600 /swapfile
```

3. 类似格式化交换分区

```bash  
mkswap /swapfile
```

4. 激活交换文件

```bash  
swapon /swapfile
```

其实这个时候通过free -h已经可以看到内存数据中的交换信息了。

5. 最后一步是在fstab中添加交换文件的信息，使系统重启以后能自动激活交换文件

```  
/swapfile none swap defaults 0 0
```

到此，打完收功。在ArchlinuxLinux的Wiki中其实是还有卸载这个交换文件的方法，但是我觉的这个用处不大，不在这里记录了，需要的时候去查就好了。
