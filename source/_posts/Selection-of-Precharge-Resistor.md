---
title: Model Selection of Pre-charge Resistor
date: 2021-04-11 18:42:53
tags:
  - Pre-charge Resistor
categories:
  - - EV
id: '9'
description: The model selection of the pre-charge resistor is very important for the pre-charge circuit designing. This article will talk about the basis for the model selection.
---
<style>
  .box {width:60%; text-align:center; font-size:10px; margin:0 auto;}
  .box img {border-radius: 10px;}
</style>

Last week I met a new issue with our vehicle: pre-charge failure. The behavior was that the negative contactor and the pre-charge relay closed then open after turn on the key. After checking the whole pre-charge circuit I found that the pre-charge resistor was damaged. This is the first time that a pre-charge failure has occurred， and of course it caught my attention.

## Principle and function of pre-charge circuit

In the drive system of an EV, the power battery is connected to a lot of high voltage components through PDU(Power Distribution Unit), such as the motor controller, OBC, DC converter, A/C(Air Condition), PTC and so on. Usually in these components there are capacitor, especially in the motor controller, the capacity of capacitor could over 2000uF. If the initial capacity is zero, once power on, it is equivalent to a short circuit, and the current is so large that the battery, contactor and others components will be damaged.

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/precharge%20circuit_new.jpg" alt="pre-charge circuit" />
</div>
