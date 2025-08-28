---
layout: post
title: Arch上配置nginx和其rmtp模块
date: 2021-10-26 10:37:00
categories: Linux
tags: Archlinux nginx
---

年初买了一本书[《直播系统开发：基于Nginx与Nginx-rtmp-module》](https://item.jd.com/12518374.html)，最近翻出来研究一下。

这本书里面的nginx和nginx-rtmp-module都是从头编译，不符合Arch人的逻辑，所以按照书里的思路，再Archlinux上重新搞一下。另外，研究了一下怎么从摄像头提取视频和音频。

首先是nginx的安装了配置。直接使用pacman –S nginx来安装nginx，然后用aur安装nginx-mod-rtmp。安装完成以后，需要编辑/etc/nginx/nginx.conf，在其第一行加入

```  
load_module "/usr/lib/nginx/modules/ngx_rtmp_module.so";
```

然后加入在http段前面加入

```  
    rtmp {
        access_log off;
        server {
            listen 1935;
            application mylive {
                live on;
            }
        }
    }
```

然后重启nginx。

这里面和书中的配置文件，主要不同在加了`access_log off`。我怀疑`nginx-mod-rtmp`的`PKGBUILD`文件关于`access_log`的默认配置有问题，导致不明确配置`access_log`的时候，会报`/etc/nginx`目录下没有权限生成`access_log`文件，并启动失败。好在我是在测试，直接关闭`access_log`就好了。这时nginx端就准备好了。

下面首先要下载一个windows下的ffmpeg的二进制包，然后先用下面命令获取ffmpeg可用的摄像头设备名称。

```bash  
ffmpeg -list_devices true -f dshow -i dummy
```

然后会出现如下图的内容。途中上面的红框里面是摄像头的内设备名称，下面是音频输入设备名称。这两个名称可以直接使用。

![](/images/2021/10/%E6%9C%AA%E5%91%BD%E5%90%8D2.jpg)

获取两个设备名以后，再用如下命令启动视频流上传：

```bash  
ffmpeg -f dshow -i video="Integrated Camera" -f dshow -i audio="麦克风阵列 (Conexant SmartAudio HD)" -vcodec libx264 -acodec aac -strict -2 -f flv rtmp://nginx:1935/mylive/6
```

这里面nginx是我的虚机的名字，如果你没有配置winbind的话，可以改用ip。如果你设备名称不一样，可以自己替换。成功后，会看到PC上摄像头的工作灯点亮，命令行中中一直有信息更新。

然后打开VLC，如下图中，选择菜单中的“媒体->打开网络串流”。

![](/images/2021/10/%E6%9C%AA%E5%91%BD%E5%90%8D3.jpg)

在弹出的对话框中，填入刚才ffmpeg发送视频流的url。

![](/images/2021/10/%E6%9C%AA%E5%91%BD%E5%90%8D4.jpg)

VLC中大约会延迟3到5秒，等几秒以后，VLC就会开始工作。下图是我同事围观的时候，拍了一张照片。

![](/images/2021/10/%E6%9C%AA%E5%91%BD%E5%90%8D.jpg)

和书中的例子相比，花了一下午的时间，才搞定。第一个坑是，网上很多人都是把mod-rtmp和nginx编译到一起了，找了半天才找到nginx怎么加载so形式的mod。第二个坑是上面`access_log`的问题。第三个坑是原书例子是使用的是一个flv文件，为了找flv视频，我找了好一会，后来又研究怎么抓本机的摄像头。

就这么多，希望对看到的朋友有帮助。

其实还有第四个坑，刚发布的时候，发现搬家以后的blog无法上传图片了，由搞了半天
