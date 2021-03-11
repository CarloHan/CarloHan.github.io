---
title: SOLVE THE WIFI CONNECTION UNSTABLE ON UBUNTU
tags:
  - connection
  - ubuntu
  - unstable
  - wifi
id: '75'
categories:
  - - Linux
date: 2020-11-13 11:36:23
---

PC: Microsoft Surface Pro 3

OS: Ubuntu 20.10

PROBLEM: WIFI disconnected when the system sleep wake, can't reconnect otherwise reboot.

REASON: Power Save service BUG

Solution:

1.  Turn off Power Management.

```
# turn off the power management
sudo iwconfig <your connection eg:wlp1s0> power off
# check the status
sudo iwconfig
  Power Management:off
```

2\. Above you will turn off the power management for one time, it will be turn on in next reboot. If you want to close it permanently:

```
# modify the power management configuration
sudo vim /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
  [connection]
  wifi.powersave = 3
# replace this value with 2, save it
# reboot, and check the status
sudo iwconfig
  Power Management:off
```

Congras, the WiFi connection will stable now.