---
title: Upgrade Procedure
tags:
  - Upgrade
categories:
  - - Mecaprom
  - - EV
top: 2
abbrlink: 14089
date: 2021-04-22 12:06:18
password: mecaprom
description: A very detailed procedure for upgrade the software on vehicle.
---

- [LMU](#lmu)
  - [Tools](#tools)
  - [Software](#software)
  - [Files](#files)
  - [Steps](#steps)
- [INVERTER](#inverter)
  - [Tools](#tools-1)
  - [Files](#files-1)
  - [Software](#software-1)
  - [Steps](#steps-1)
- [BMS](#bms)
  - [Tools](#tools-2)
  - [Software](#software-2)
  - [Files](#files-2)
  - [Steps](#steps-2)
- [LMU Software Version Check](#lmu-software-version-check)
  - [Tools](#tools-3)
  - [Software](#software-3)
  - [Steps](#steps-3)
- [Annotate](#annotate)
  - [HW](#hw)
    - [OBD Cable](#obd-cable)
    - [CANUSB Adapter](#canusb-adapter)
    - [Kvaser Leaf Light V2](#kvaser-leaf-light-v2)
    - [INONE USBCANII](#inone-usbcanii)
  - [SW](#sw)
    - [Upgrade Files Folder](#upgrade-files-folder)
    - [McpProgramInterface.jar](#mcpprograminterfacejar)
    - [Glelec Flash DownLoad.exe](#glelec-flash-downloadexe)
    - [INONE BMS Calibrate](#inone-bms-calibrate)
    - [BusMaster](#busmaster)
    - [HEX 2 DEC Convert](#hex-2-dec-convert)

<style>
.box {
    width: 40%;
}
.small {
    width: 20%
}
img{
    width: 70%;
}
</style>

!!! Attention
    Please use the internal hyperlink to read this article.

## LMU

### Tools

- [OBD cable](#obd-cable)
- [CANUSB adapter](#canusb-adapter)
- PC

### Software

- [McpProgramInterface.jar](#mcpprograminterfacejar)

### Files

- [SW_VERSION_OFFICIAL](#upgrade-files-folder)

### Steps

1. Turn OFF the key.
2. Connect PC and vehicle through [OBD cable](#obd-cable) and [CANUSB adapter](#canusb-adapter), use the 'traction CAN'.
3. Run the software [McpProgramInterface.jar](#mcpprograminterfacejar).
4. Upgrade the LMU according to the [procedure](#mcpprograminterfacejar).
5. Disconnect the cables and restart the vehicle.

## INVERTER

### Tools

- [OBD cable](#obd-cable)
- [Kvaser Leaf Light V2](#kvaser-leaf-light-v2)
- PC

### Files

- [INVERTER_UPGRADE_OFFICIAL](#upgrade-files-folder)

### Software

- [Glelec Flash DownLoad.exe](#glelec-flash-downloadexe)

### Steps

1. Turn OFF the key.
2. Connect PC and vehicle through OBD cable and Kvaser Leaf Light V2, use the 'traction CAN'.
3. Run the software [Glelec Flash DownLoad.exe](#glelec-flash-downloadexe).
4. Upgrade the Inverter according to the [procedure](#glelec-flash-downloadexe).
5. Disconnect the cables and restart the vehicle.

## BMS

### Tools

- [OBD cable](#obd-cable)
- [USBCANII adapter](#inone-usbcanii)
- PC

### Software

- [INONE BMS Calibrate](#inone-bms-calibrate)

### Files

- [BMS_UPGRADE_OFFICIAL](#upgrade-files-folder)

### Steps

1. Turn ON the key.
2. Connect PC and vehicle through OBD cable and INONE USBCANII, use the 'BMS debug CAN'.
3. Run the software [INONE BMS Calibrate.exe](#inone-bms-calibrate).
4. Upgrade the BMS according to the [procedure](#inone-bms-calibrate).
5. Disconnect the cables and restart the vehicle.

## LMU Software Version Check

### Tools

- [OBD cable](#obd-cable)
- [Kvaser Leaf Light V2](#kvaser-leaf-light-v2)
- PC

### Software

- [BusMaster](#busmaster)

### Steps

1. Turn ON the key.
2. Connect PC and vehicle through OBD cable and Kvaser Leaf Light V2, use the 'traction CAN'.
3. Run the software [BusMaster](#busmaster).
4. Read the message [0x210](#hex-2-dec-convert).
5. Convert the 6th Byte from hex to decimal via the [Windows Calculator](#hex-2-dec-convert), then you will get the version number.

## Annotate

### HW

#### OBD Cable

There are 3 channels of CAN from the OBD cable: traction CAN, charge CAN and BMS debug CAN. <br/>
![OBD cable](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/OBD%20cable.jpeg)

#### CANUSB Adapter

![CANUSB Adapter](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/USBCAN.jpeg)

#### Kvaser Leaf Light V2

![Kvaser leaf light V2](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/kvaser.jpeg)

#### INONE USBCANII

![INONE USBCANII](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/INONE%20USBCANII.jpeg)

### SW

To upgrade LMU, INVERTER and BMS, the software and files are required. <br/>

<img class="box" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413122605.png" alt="Upgrade softwares" />

#### Upgrade Files Folder

All of official version software for upgrade are placed in the folder 'Upgrade', the structure of this folder is as bellow: <br/>

![Upgrade folder structure](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413122013.png)

#### McpProgramInterface.jar

This software was developed using Java language, it means that to running it the JRE(Java Runtime Environment) is required. <br/>

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413124607.png" alt="McpProgramInterface" />

1. Make sure the vehicle is turned off.
2. Double click the icon to run the program.
3. Select the CANUSB adapter: <br/>
   ![Upgrade LMU 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413125557.png) <br/>
   ![Upgrade LMU 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413125806.png) <br/>
   ![Upgrade LMU 04](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413130131.png)
4. Select the official software: <br/>
   ![Upgrade LMU 05](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413135839.png)
5. Turn on the vehicle, and the updating will start automatic: <br/>
   ![Upgrade LMU 06](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413141038.png) <br/>
   ![Upgrade LMU 07](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413141555.png)
6. Close the program.

#### Glelec Flash DownLoad.exe

This software was provided from the supplier of inverter, it was used for updating the inverter. <br/>

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413142342.png" alt="Glelec Flash DownLoad" />

1. Make sure the vehicle is turned off.
2. Double click the icon to run this program.
3. The language of the application is in Chinese, don't worry, what you only need to do is select the updating file and run: <br/>
   ![Upgrade INVERTER 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413143005.png) <br/>
   ![Upgrade INVERTER 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413143144.png)
4. Turn on the vehicle, click the button to start flashing: <br/>
   ![Upgrade INVERTER 04](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413143608.png) <br/>
   ![Upgrade INVERTER 05](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413143831.png) <br/>
   ![Upgrade INVERTER 06](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413144051.png)
5. Close the program.

#### INONE BMS Calibrate

This software was provided from the supplier of BMS, it was used for updating the BMS. <br/>

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413144317.png" alt="INONE BMS Calibrate" />

1. Make sure the vehicle is turned on.
2. Double click the icon to run the program.
3. Start the program with the default setting: <br/>
   ![Upgrade BMS 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/INONE%2002.png)
4. Go to 'Upgrade' page: <br/>
   ![Upgrade BMS 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413145254.png) <br/>
   ![Upgrade BMS 04](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413145628.png) <br/>
   ![Upgrade BMS 05](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413145931.png)
5. Close the program.

<div class="admonition tldr">
  <p class="admonition-title">BMS Software Version</p>

|        | With Emerg            | No Emerg              |
| ------ | --------------------- | --------------------- |
| 40S32P | JDI2008120503_V2.0.3  | JDI2008120503_V1.0.3  |
| 42S28P | JDI2008120504_V2.0.14 | JDI2008120504_V1.0.14 |
</div>

#### BusMaster

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster.PNG" alt="BusMaster" />

BusMaster is a simple but useful application for CAN bus diagnostic and the features it has are enough for 80% daily requirements.

1. Connect Kvaser with PC.
2. Run BusMaster: <br/>
   ![BusMaster 01](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_01_new.png)<br/>
   ![BusMaster 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_02.png)<br/>
   ![BusMaster 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_03.png)
3. Add database: <br/>
   ![BusMaster 04](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_04.png)<br/>
   ![BusMaster 05](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_05.png)<br/>
   ![BusMaster 06](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_06.png)
4. After starting, there are all of the CAN messages around CAN bus, don't worry because only tew of them have to be focused: <br/>
   ![BusMaster 07](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_07.png)<br/>
   ![BusMaster 08](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_08.png)<br/>
   ![BusMaster 09](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/BusMaster_09.png)

#### HEX 2 DEC Convert

To check the software version of LMU, at first you must read a message via BusMaster: <br/>

<div class="admonition tldr">
  <p class="admonition-title">ID 0x600 LMU_FAULT_STS</p>

  ![LMU VERSION BUSMASTER](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210415151714.png) <br/>

  <p> ID: 0x210, UO1_Io_Cmd, Byte 6 </p>
</div>

The number you got is in hex, then you have to convert it to decimal via Microsoft Calculator: <br/>

1. Run Microsoft Calculator, click the hamburger icon on the top left, select 'Programmer' mode. <br/>
   <img class="box" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210415152749.png" alt="Windows Calculator 01" />
2. Select HEX and enter the number you read from CAN message. <br/>
   <img class="box" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210415153013.png" alt="Windows Calculator 02" />
3. Then you will get the decimal number at once.

---

> Company: MECAPROM
> Author: YING.H
> Date: 15/04/2021
> Version: 1.1
> Changelog: V1.1 Add LMU version check
