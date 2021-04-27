---
title: A Concise Introduction to the EV Charging Process(MODE-3)
tags:
  - EV
  - Charging
  - MODE 3
categories:
  - - EV
top: 30
abbrlink: 49106
date: 2021-04-26 10:47:08
description: This article will try to introduce the EV charging process in a perspicuity manner via a real case.
---

<style>
  .box {width:60%; text-align:center; font-size:10px; margin:0 auto;}
  .box img {border-radius: 10px;}
</style>

Recently I got a feedback from a customer said the EVSE they owner cannot charge our vehicle. The behavior is when the connector plugged, the EVSE goes to the error status at once. Then he send a the model of the charger is as follow:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210427142820.jpg" alt="Efacec EV-HC3" />
  Efacec EV-HC3 EVSE
</div>

Searching on the internet, I got that this charger's model is **efacec EV-HC3 G3**, the main features as bellow:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210427162102.jpg" alt="Efacec Charger datasheet" />
  Datasheet of the Efacec EV-HC3 Charger
</div>

Seeing as either the charger or the BMS was designed according to IEC61851, why doesn't it work? What's more bizarre is the charger we provide along with the vehicle is working well with either our vehicle or others, the charger they have can work with other vehicle as well. To find the key point out, I decided to record the charging process via both of the software and hardware.

<iframe width="560" height="315" src="https://www.youtube.com/embed/lEgg_gGY_Pw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
