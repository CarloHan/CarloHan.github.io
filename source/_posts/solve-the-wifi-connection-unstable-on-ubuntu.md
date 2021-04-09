---
title: Solve The Problem of Unstable WiFi Connection On Ubuntu OS
tags:
  - Ubuntu
  - WiFi
  - Surface Pro
id: '5'
categories:
  - - Linux
date: 2020-11-13 11:36:23
description: After a period of hard word, I install Ubuntu OS on my Microsoft surface Pro 3 successfully. However, there are a few ghost failures taht greatly affect the user experience, such as WiFi connection unstable.
---

## Description

+ PC: Microsoft Surface Pro 3
+ OS: Ubuntu 20.10
+ PROBLEM: After the system wakes up from sleep, WiFi cannot automatically reconnect unless restarted
+ REASON: Power Save service BUG

## Solution

### Temporary

Turn off Power Management

```shell
# turn off the power management
sudo iwconfig <your connection eg:wlp1s0> power off
# check the status
sudo iwconfig
  Power Management:off
```

### Permanent

Above you will turn off the power management for one time, it will turn on in next reboot. If you want to close it permanently:

```shell
# modify the power management configuration
sudo vim /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
  [connection]
  wifi.powersave = 3
# replace this value with 2, save it
# reboot, and check the status
sudo iwconfig
  Power Management:off
```

Congrats, the WiFi connection will be stable now.
