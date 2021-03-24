---
title: How to modify the volume of EBS on AWS
tags:
  - aws
  - expand
  - volum
id: '44'
categories:
  - - Linux
date: 2020-10-25 11:38:09
description: 
---

When I created my EC2 instance, since the limitation of free version, I allocated only 8GB to the root volume. I soon realized that this volume was almost used up.

As the free instance, Amazon gave us 30GB size to be used. It's better estimate the size according to your purpose before allocate.

Anyway, if you have the same problem, dont worry, let's see how to expand it within 3 steps.

## Modify the volume size on the EC2 dashboard

![AWS DASHBOARD](https://www.niceying.com/wp-content/uploads/2020/10/微信图片_20201025095840.png)

a. On the dashboard, select "ELASTIC BLOCK STORE - Volumes".

![AWS EBS](https://www.niceying.com/wp-content/uploads/2020/10/微信图片_20201025095805.png)

b. Right click the volume which you want to modify, select "Modify Volume".

![Modify volume](https://www.niceying.com/wp-content/uploads/2020/10/微信图片_20201025100644.png)

c. Enter the volume size you want to reset, pay attention if you're using a free instance, the total size don't over 30GB, otherwise you will receive the bill from Amazon.

2\. Login your instance to modify partition.

![lsblk](https://www.niceying.com/wp-content/uploads/2020/10/1548507836-5c2c2c17db432_articlex.png)

a. From ssh login to your instance, enter command "`lsblk`", you will see the real size of all volumes and the partitions. You will see that the size of the volume has been modified, but the patition has not used all of the volume yet.

![growpart command](https://www.niceying.com/wp-content/uploads/2020/10/3128725125-5c2c2c196dada_articlex.png)

b. Enter command "`sudo growpart /dev/xvda 1`", to make partition "xvda1" use all of the volume available.

![lsblk](https://www.niceying.com/wp-content/uploads/2020/10/2109384238-5c2c2c178ead5_articlex.png)

c. Now you can see that the partition size is equal to the volume size. But...

3\. Ajust the filesystem.

![filesystem not recognize the new space](https://www.niceying.com/wp-content/uploads/2020/10/2922913778-5c2c2c15389c6_articlex.png)

a. But the filesystem has not yet recognized this new space, therefor we have to tell him through the command "`sudo resize2fs /dev/xvda1`". (if your filesystem shows as /dev/root, you should use "`sudo resize2fs /dev/root`")

![expand done](https://www.niceying.com/wp-content/uploads/2020/10/微信图片_20201025111614.png)

b. Congratulations, the volume has been expanded.

PS: Because I forgot screenshot the picture when I was procesing, so there is a few pictures from internet. If it violates your rights, please let me know and I will delete it.