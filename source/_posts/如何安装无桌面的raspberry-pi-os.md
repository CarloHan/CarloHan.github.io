---
title: How to Install a Headless Raspberry Pi OS
tags:
  - Headless
  - raspberry OS
top: 22
categories:
  - - Raspberry
description: >-
  In order to running OpenCV more faster on Raspberry Pi, I have to reinstall
  the Raspberry Pi OS with the headless version. With this version, the Raspberry Pi
  will no longer have a GUI(desktop), and you have to talk with him through
  headless mode, which means SSH. In this case, the initial configuration is
  very important.
abbrlink: 7170
date: 2020-10-12 23:22:07
---

最近把个人博客转移到AWS上去，于是手头的Raspberry Pi 4B就闲了下来，正好还有一个Pi使用的摄像头，就准备拿来熟悉一下OpenCV。

由于之前为了安装宝塔面板，使用了OPENFANS发布的[Debian-Pi-Aarch64](https://gitee.com/openfans-community/Debian-Pi-Aarch64)系统，索性重新制作一遍系统。因为TF卡比较小，最终选择了无桌面的官方系统。

## 制作系统镜像

第一步把系统镜像烧写到TF卡，由于官方提供了[Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)，制作过程变得非常简单。

![Raspberry Pi Imager](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/raspberry%20pi%20image.png)

只需将TF卡插在电脑上，然后打开Raspberry Pi Imager，选择你想制作的系统，再选择TF卡，点击写入，等待写入完成即可。

## 提前配置网络环境

下面重点来了，因为是无桌面系统，不能连接显示器键盘鼠标来进行wifi连接，账号设置等操作，所以需要使用ssh进行连接，并手动配置wifi。

系统写入完成后，不要拔出TF卡，直接在电脑上打开TF卡，在root根目录下，新建一个文本文档取名为ssh并删掉后缀.txt。之后再新建一个文本文档取名为wpa\_supplicant，后缀.conf，使用VScode或其他编辑器打开这个文档，在里面进行wifi配置如下：

```shell
country=IT    #所在国家代码
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={     #使用network可添加多个wifi，根据priority优先级依次连接
 ssid="<WiFi名,不能有中文>" 
 psk="<密码>" 
 priority=10 
}
 
network={
 ssid="<第二个WiFi名>"
 psk="<第二个密码>" 
 priority=<替换成数字，数字越大代表优先级越高> 
```

至此，前戏部分就结束了，将TF卡拔出，插在Pi上，然后接通电源，看到黄灯闪烁则系统运行成功。下一步需要找到你的Pi所分配到的IP地址，进行ssh连接。
