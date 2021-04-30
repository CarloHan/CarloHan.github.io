---
title: A Concise Introduction to the EV Charging Process
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

Seeing as either the charger or the BMS was designed according to IEC 61851, what's more bizarre is the charger we provide along with the vehicle is working well with either our vehicle or others, the charger they have can work with other vehicle as well. Why doesn't it work?

## IEC 61851

To analyze the process, let's study the standard at first. You may heard variety difference standard about EV charging, such as SAE J1772, IEC 62196, IEC 61851 and so on. What we need to focus on is the signaling protocol, IEC 61851 introduces and describes the specific function.

### Signaling circuit

Below is the electrical schematic diagram of the signaling circuit:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210430150310.gif" alt="Signaling circuit" />
  Electrical schematic diagram of the signaling circuit
</div>

This diagram shows a SAE J1772 connector, there are 5 pins through the connection. Pin 1 is Live wire, Pin 2 is Neutral wire, Pin 3 is PE(Protective Earth), Pin 4 is CP(Control Pilot) and Pin 5 is PP(Proximity Pilot). Before plugging the connector, the EVSE controller puts constant $+12V$ on CP. Once the connector was plugged, the current loop CP-PE is connected permanently on the vehicle side via a $2.74k\Omega$ resistor($R3$), and it making a voltage drop down from $+12V$ to $+9V$. The EVSE controller detected the voltage difference, switch($K2$) the constant supply to a $1kHz$ square wave($PWM$, amplitude $\pm12V$). The charging will be activated by the vehicle by adding parallel $1.3k\Omega$ resistor($R2$) resulting in a voltage drop to $+6V$, or by adding a parallel $270\Omega$ resistor for a required ventilation resulting in a voltage drop to $+3V$. Once the EVSE detected the activated voltage, the relay on the Neutral wire and Live wire is closed, and the charging start. The following table shows the threshold for different states.

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210430225739.jpg" alt="Pilot signal states" />
  Pilot signal states
</div>

In fact, all of the voltage out of the range will be considered an error.

### Current limit

Obviously for a $PWM$, it is worth noting only the amplitude, but also the duty cycle. The charging station can use the duty cycle to describe the maximum current that is available:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210430234838.jpg" alt="Ampere capacity with PWM duty cycle" />
  Ampere capacity with PWM duty cycle
</div>

From the log it shows that there was no PWM sent from the efacec's charger after plugged the connector, but for the charger we provide there was PWM. Since BMS cannot detect PWM, the charging process will not go ahead, then the charger give an error.

To 
<iframe width="560" height="315" src="https://www.youtube.com/embed/lEgg_gGY_Pw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
