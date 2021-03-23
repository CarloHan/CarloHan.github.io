---
title: An old electronic flasher for automotive
tags:
  - analog cicuit
  - flasher
  - multivibrator
id: '61'
categories:
  - - HW
date: 2021-01-12 17:46:50
description: Analyzing and simulating the working principle of an old electronic flasher.
---

![Electronic flasher](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/an%20old%20flasher.jpeg)

Last month I opened an electronic flasher for automotive, it's an old version which designed by transister, not IC. I have been busy testing a new BMS all month, and until now I have no time to talk about this component. The schematic copy as below.

![Schematic flasher](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/flasher%20schematic.png)

Schematic copy

Pin B is the positive 12V, pin E is ground, pin L is connected to a direction light lever. It was replaced by a 820ohm resistor. Let's see what will happen in the simulation.

<center>
  <img style="border-radius: 0.3125em;
  box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
  src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/flasher%20simulate.png" width = "65%" alt=""/>
  <br>
  <div style="color:orange; border-bottom: 1px solid #d9d9d9;
  display: inline-block;
  color: #999;
  padding: 2px;">
    Voltage(LED) - T
  </div>
</center>

The direction light flashes every 300 ms, and there is no clock no timer no mcu, only a little basic electronic components. Let's analyse how it is realized.
