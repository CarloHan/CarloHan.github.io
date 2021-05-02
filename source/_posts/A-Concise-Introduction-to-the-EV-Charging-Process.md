---
title: Revisited the EV Charging Process
tags:
  - EV
  - Charging
  - IEC 61851
  - CP
categories:
  - - EV
top: 30
abbrlink: 49106
mathjax: true
date: 2021-04-26 10:47:08
description: This article will try to introduce the EV charging process in a perspicuity manner via a real case.
---

<style>
  .box {width:60%; text-align:center; font-size:10px; margin:0 auto;}
  .box img {border-radius: 10px;}
</style>

Recently I got a feedback from a customer said the EVSE they owned(**charger 1**) cannot charge our vehicle. The performance is when the connector plugged, the EVSE goes to the error status at once. Then he send the model of the charger to me:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210427142820.jpg" alt="Efacec EV-HC3" />
  Efacec EV-HC3 EVSE
</div>

Searching on the internet, I got that this charger's model is **efacec EV-HC3 G3**, the main features as bellow:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210427162102.jpg" alt="Efacec Charger datasheet" />
  Datasheet of the Efacec EV-HC3 Charger
</div>

Seeing as either the charger or the BMS was designed according the same standard, what's more bizarre is the charger we provide along with the vehicle(**charger 2**) is working well with either our vehicle or others, the charger they have can work with other vehicle as well, but why does it can't work with our vehicle?

## IEC 61851

To analyze this issue, let's study the standard at first. You may heard variety difference standard about EV charging, such as SAE J1772, IEC 62196, IEC 61851 and so on. What we need to focus on is the signaling protocol, IEC 61851 introduces and describes the specific function.

### Signaling circuit

Below is the electrical schematic diagram of the signaling circuit:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210430150310.gif" alt="Signaling circuit" />
  Electrical schematic diagram of the signaling circuit
</div>

This diagram shows a SAE J1772 connector, there are 5 pins through the connection. Pin 1 is Live wire, Pin 2 is Neutral wire, Pin 3 is PE(Protective Earth), Pin 4 is CP(Control Pilot) and Pin 5 is PP(Proximity Pilot). 

Before plugging the connector, the EVSE controller puts constant $+12V$ on CP. Once the connector was plugged, the current loop CP-PE is connected permanently on the vehicle side via a $2.74k\Omega$ resistor($R3$), and it making a voltage drop down from $+12V$ to $+9V$. The EVSE controller detected the voltage difference, switch($K2$) the constant supply to a $1kHz$ square wave($PWM$, amplitude $\pm12V$). The charging will be activated by the vehicle by adding parallel $1.3k\Omega$ resistor($R2$) resulting in a voltage drop to $+6V$, or by adding a parallel $270\Omega$ resistor for a required ventilation resulting in a voltage drop to $+3V$. Once the EVSE detected the activated voltage, the relay on the Neutral wire and Live wire is closed, and the charging start. The following table shows the threshold for different states.

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210430225739.jpg" alt="Pilot signal states" />
  Pilot signal states
</div>

In fact, for any voltage out of the range will be considered as an error.

### Current limit

Obviously for a $PWM$, it is worth noting only the amplitude, but also the duty cycle. The charging station can use the duty cycle to describe the maximum current that is available:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210430234838.jpg" alt="Ampere capacity with PWM duty cycle" />
  Ampere capacity with PWM duty cycle
</div>

## Testing

Now let's look back at the case we mentioned in the beginning. To find the key of this issue, I recorded the CP states on vehicle side via PicoScope when the two chargers were plugged.

### Charger 1 (the charger owned by client)

<iframe width="560" height="315" src="https://www.youtube.com/embed/s0OlHtV7aTE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

From this video we got that there was a voltage drop down when the connector plugged(initially $+12V$), but why the process get stuck?

The standard specifies that the voltage judgement range of State B(vehicle detected) is $9\pm1V$. It the video, the voltage dropped to around $7.9V$, it was out of the range. In this case, the EVSE cannot ensure the vehicle has been connected, thus it will not activate the wave generator, as well as the vehicle don't adding the parallel resistor since no PWM was detected.

### Charger 2 (the charger we provide)

<iframe width="560" height="315" src="https://www.youtube.com/embed/lEgg_gGY_Pw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In this video, the behavior of the signal is definitely correct at first glance, and of course the charger can charge the vehicle. However, if you watch the video carefully, you will find that there is a big problem: the amplitude. At state B, the voltage drop to $7.9V$, out of range, at state C, the voltage drop to $5.1V$, it's just at critical points, but this charger has made a correct judgement on both states. It means this charger give a wide threshold for each state. And this is the main reason why we did not meet this problem during the debugging phase.

## Analysis

The CP-PE is a very simple loop consists only a supply on EVSE side, resistors and a sampling circuit on BMS to detect the signal from EVSE. Thus the problem should be the consumption of the sampling circuit. The testing results is as follow:

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210502162411.jpg" alt="Charging sampling circuit" />
  CP current loop analysis
</div>

Ideally, the current of sampling circuit should be zero, hence:

$$ V_{T1} = 12V - (1k\Omega * 2.71mA) = 9.29V $$

However, in the actual circuit, the current flowing through the sampling circuit is as high as $1.28mA$, in this case:

$$ V_{T1} = 12V - (1k\Omega * (2.71 + 1.28)mA) = 8V $$

Obviously, excessive consumption of the sampling circuit leads to excessive voltage drop of the resistor $R1$.

## Solution

In order to reduce the consumption of the sampling circuit, a simple solution is  replaced the BJT with 2N7002k, a N-channel enhancement type MOSFET, to increase the input impedance.

<div class="box">
  <img src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210502175751.jpg" alt="Charging sampling circuit" />
  Sampling BJT: Q203, Q205
</div>

By dealing with this issue, I revisited the EV charging standard and have a clearer understanding. Also for the hardware design, it must be verified by the worst condition and must meet the requirements of standard. If you have any doubt with EV charging, please leave it in the comment then we will discuss together.