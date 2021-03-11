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
---

![Electronic flasher](https://www.niceying.com/wp-content/uploads/2020/10/微信图片_20201027110559-scaled.jpg)

Last month I opened an electronic flasher for automotive, it's an old version which designed by transister, not IC. I have been busy testing a new BMS all month, and until now I have no time to talk about this component. The schematic copy as below.

![](https://www.niceying.com/wp-content/uploads/2020/11/微信图片_20201102101332.png)

Schematic copy

Pin B is the positive 12V, pin E is ground, pin L is connected to a direction light lever. It was replaced by a 820ohm resistor. Let's see what will happen in the simulation.

![](https://www.niceying.com/wp-content/uploads/2020/11/微信图片_20201102101739.png)

Voltage(LED) - T

The direction light flashes every 300 ms, and there is no clock no timer no mcu, only a little basic electronic components. Let's analyse how it is realized.