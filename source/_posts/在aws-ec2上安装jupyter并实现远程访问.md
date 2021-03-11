---
title: 在AWS EC2上安装Jupyter并实现远程访问
tags:
  - aws
  - jupyter
id: '30'
categories:
  - - Linux
date: 2020-10-09 17:31:01
---

最近准备在AWS上安装Jupyter服务器实现远程访问，本以为很简单的事情竟遇到了许多坑，花了一天的时间也没有解决掉。。。

最终在jupyter的[论坛](https://medium.com/@alexjsanchez/python-3-notebooks-on-aws-ec2-in-15-mostly-easy-steps-2ec5e662c6c6)上找到了一个解决办法：

```
ssh -i <your key.pem> -NfL <local port>:localhost:<server port> <user@ip>
```

使用ssh -NfL端口转发，将jupyter在远程服务器的端口转发到本地端口。