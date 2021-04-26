---
title: A Command to Solve the Issue of Remote Access the Jupyter Servers Running on AWS
tags:
  - AWS
  - Jupyter
top: 23
categories:
  - - Linux
description: >-
  I have wasted a day to access the Jupyter remote server on my AWS, finally
  it was solved by a simple command. Hope this article could help you to save
  your time.
abbrlink: 2314
date: 2020-10-09 17:31:01
---

Recently I try to install the Jupyter server on the AWS to achieve a remote access. I thought it was a very little case but encountered a lot of problems and spent almost a day to solve them.

Finally, in the [forum of Jupyter](https://medium.com/@alexjsanchez/python-3-notebooks-on-aws-ec2-in-15-mostly-easy-steps-2ec5e662c6c6) I found a very simple but effective solution：

```shell
ssh -i <your key.pem> -NfL <local port>:localhost:<server port> <user@ip>
```

It use command```-NfL```to forward the port of the remote server to the local port.

Try to solve and share the problems you met during the deployed in the comment.
