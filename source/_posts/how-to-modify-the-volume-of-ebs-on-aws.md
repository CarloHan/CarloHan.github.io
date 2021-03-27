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
description: Thanks to Amazon's generosity that we can use a cloud host for free in one year. Although there are few resources available, it is enough for most amateur users just like me. In order to allocate the 30GB volume more reasonably, sometimes you need to adjust it.
---

<style>
  .box {width:60%; text-align:center; font-size:10px; margin:0 auto;}
  .box img {border-radius: 10px;}
</style>

When I created my EC2 instance, since the limitation of free version, I allocated only 8GB to the root volume. I soon realized that this volume was almost used up.

As the free instance, Amazon gave us 30GB size to be used. It's better estimate the size according to your purpose before allocate.

Anyway, if you have the same problem, dont worry, let's see how to expand it within 3 steps.

## Modify the volume size on the EC2 dashboard

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20201025095840.png" alt="AWS DASHBOARD"/>
</div>

1. On the dashboard, select "ELASTIC BLOCK STORE - Volumes".

   <div class="box">
     <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20201025095805.png" alt="AWS EBS"/>
   </div>

2. Right click the volume which you want to modify, select "Modify Volume".

   <div class="box">
     <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20201025100644.png" alt="Modify volume"/>
   </div>

3. Enter the volume size you want to reset, pay attention if you're using a free instance, the total size don't over 30GB, otherwise you will receive the bill from Amazon.

## Login your instance to modify partition

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/1548507836-5c2c2c17db432_articlex.png" alt="lsblk"/>
</div>

1. From ssh login to your instance, enter command "`lsblk`", you will see the real size of all volumes and the partitions. You will see that the size of the volume has been modified, but the patition has not used all of the volume yet.

   <div class="box">
     <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/3128725125-5c2c2c196dada_articlex.png" alt="growpart command"/>
   </div>

2. Enter command "`sudo growpart /dev/xvda 1`", to make partition "xvda1" use all of the volume available.

   <div class="box">
     <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/2109384238-5c2c2c178ead5_articlex.png" alt="lsblk"/>
   </div>

3. Now you can see that the partition size is equal to the volume size.

## Ajust the filesystem

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/2922913778-5c2c2c15389c6_articlex.png" alt="filesystem not recognize the new space" />
</div>

1. But the filesystem has not yet recognized this new space, therefor we have to tell him through the command "`sudo resize2fs /dev/xvda1`". (if your filesystem shows as /dev/root, you should use "`sudo resize2fs /dev/root`")

   <div class="box">
     <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20201025111614.png" alt="expand done" />
   </div>

2. Congratulations, the volume has been expanded.

PS: Since I forgot to screenshot the picture when I was procesing, there is a few pictures from internet. If it violates your rights, please let me know and I will delete them.
