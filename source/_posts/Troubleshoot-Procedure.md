---
title: Troubleshoot Procedure
tags:
  - Troubleshoot
categories:
  - - Mecaprom
  - - EV
top: 1
password: mecaprom
description: A very detailed procedure for the vehicle's troubleshooting
abbrlink: 41237
date: 2021-04-23 10:29:13
---

- [Warning or error shows on dashboard](#warning-or-error-shows-on-dashboard)
  - [Typical Procedure](#typical-procedure)
    - [Tools](#tools)
    - [Software](#software)
    - [Steps](#steps)
  - [Data Logging](#data-logging)
    - [Tools](#tools-1)
    - [Software](#software-1)
    - [Steps](#steps-1)
- [Others](#others)
  - [CAN Communication Error](#can-communication-error)
  - [Wiring Harness Fault](#wiring-harness-fault)
  - [Components Damage](#components-damage)
  - [Data Analyze](#data-analyze)
- [Annotate](#annotate)
  - [HW](#hw)
    - [Kvaser Leaf Light V2](#kvaser-leaf-light-v2)
    - [OBD Cable](#obd-cable)
    - [VECTOR GL2000 CAN/LIN Data Logger](#vector-gl2000-canlin-data-logger)
    - [INONE USBCANII](#inone-usbcanii)
    - [PicoScope](#picoscope)
  - [SW](#sw)
    - [BusMaster](#busmaster)
    - [INONE BMS Calibrate](#inone-bms-calibrate)
    - [Vector Logger Configurator](#vector-logger-configurator)
      - [Initialize Configuration](#initialize-configuration)
      - [Export Data](#export-data)
    - [Data Analyze by Vector CANalyzer](#data-analyze-by-vector-canalyzer)
  - [CAN Communication](#can-communication)
    - [Channels](#channels)
    - [Terminal Resister](#terminal-resister)
    - [Signal Characteristic](#signal-characteristic)
  - [CAN Message 0x2E0 and 0x600](#can-message-0x2e0-and-0x600)
  - [Fault Lists](#fault-lists)

---

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

## Warning or error shows on dashboard

This is the most common behavior when the vehicle have a problem with the electrical, control units or communication. The pictures are as follows:

![dashboard fault](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/dashboard%20fault.png)

Or:

![dashboard error](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/dashboard%20error.png)

In this case, please deal it according to the [typical procedure](#typical-procedure).  

### Typical Procedure

#### Tools

- [Kvaser leaf light V2](#kvaser-leaf-light-v2)
- [OBD cable](#obd-cable)
- [INONE USBCANII](#inone-usbcanii)
- [PicoScope](#picoscope)
- PC
- Multimeter

#### Software

- [BusMaster](#busmaster)
- [INONE BMS Calibrate](#inone-bms-calibrate)

#### Steps

1. Connect the computer and vehicle through OBD cable and Kvaser, pay attention that the CAN channel to be used is [Traction CAN](#can-communication).
2. Read CAN message by [BusMaster](#busmaster).
3. Follow two messages: [0x2E0 and 0x600](#can-message-0x2e0-and-0x600).
4. Search the fault description in the [fault lists](#fault-lists).
5. Analyze the fault and try to solve it.

### Data Logging

In general, 90% of problems can be solved through the typical procedure, however, sometimes it cannot be detected intuitively, such as a software logical error. In this case, recording CAN message is required.

#### Tools

- [VECTOR GL2000 CAN/LIN Data Logger](#vector-gl2000-canlin-data-logger)
- [OBD cable](#obd-cable)
- 12V power supply

#### Software

- [Vector Logger Configurator](#vector-logger-configurator)

#### Steps

1. [Initialize vector GL2000](#initialize-configuration).
2. Connect it to vehicle through an OBD cable, and supply it by a 12V battery.
3. Driving the vehicle to record data, and mark the time when an error occurred.
4. Disconnect it then [export the data](#export-data).

## Others

### CAN Communication Error

Since hardware or software problem, one of the node was offline from the BUS. In this case, the processing flow is as follows:

1. Check which node lost via [message 0x600](#fault-lists).
2. Check if the CAN wiring of this node is correct.
3. Check if the terminal resistor is ok.
4. Check if the characteristic of CAN signal wave is normal via PicoScope.  

### Wiring Harness Fault

Due to the relatively small purchase in the early stages of production, the supplier may make some mistakes during produce the wiring harness. It will cause some unexpected electric error. In this case, please check the wiring connection and pin position on the related connectors according to the _vehicle electric schematic_.

### Components Damage

Sometimes, due to the quality inspection of supplier is not strict, there may be some components doesn't work. In this case, if the wiring harness is ok, try to replace it with a new one.

### Data Analyze

In general, this work will be done by the colleagues of Sareno, because the software was developed by them and they can find the fault out faster. However, sometime the problem is obviously and it can be found out through your experience to save a lot of time, thus, it is recommended to learn the basic knowledge of the [Vector CANalyzer](#data-analyze-by-vector-canalyzer).

## Annotate

### HW

#### Kvaser Leaf Light V2

![Kvaser leaf light V2](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/kvaser.jpeg)

#### OBD Cable

![OBD cable](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/OBD%20cable.jpeg)

#### VECTOR GL2000 CAN/LIN Data Logger

![VECTOR GL2000 Data Logger](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/vector%20data%20logger.jpeg)

#### INONE USBCANII

![INONE USBCANII](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/INONE%20USBCANII.jpeg)

#### PicoScope

![PicoScope](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210415091226.jpeg)

### SW

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

#### INONE BMS Calibrate

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210413144317.png" alt="INONE 01" />

INONE BMS calibrate is a software to calibrate parameters of BMS and check status of BMS.

1. Connect INONE USBCANII to PC.
2. Run INONE BMS calibrate: <br/>
   ![INONE 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/INONE%2002.png)
   ![INONE 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/INONE%2003.png)

#### Vector Logger Configurator

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/Vector%20Logger%20Configurator.PNG" alt="Vector Logger Configurator" />

Vector logger configurator is a software specially used to configure Vector Logger.

##### Initialize Configuration

Before using vector GL2000, it must be initialized:

1. Connect the vector GL2000 to the PC.
2. Select driver: <br/>
   ![Configurations 01](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/initial%2001_new.PNG)<br/>
   ![Configurations 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/initial%2002.PNG)<br/>
   ![Configurations 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/initial_03_new.PNG)<br/>
   ![Configurations 04](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/initial_04.PNG)<br/>
   ![COnfigurations 05](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/initial_05.PNG)
3. Disconnect the vector GL2000.

##### Export Data

After recording, the data must be exported from vector GL2000 and save as a BLF logging file:

1. Disconnect vector GL2000 after all the lights on it to go out from vehicle.
2. Connect it with PC.
3. Export the data through Vector Logger Configurator: <br/>
   ![Export 01](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/export_01.PNG)
4. After export has been done, remember initialize the vector GL2000 for the next time using.

#### Data Analyze by Vector CANalyzer

<img class="small" src="https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_01.PNG" alt="CANalyzer 01" />

The Vector CANalyzer can be used to analyze CAN messages in online or offline mode. We usually use it in offline mode. In this mode, CANalyzer will read the log file that you recorded by vector GL2000 and replay it in order to be analyzed.

1. Measurement setup <br/>
   ![CANalyzer 10](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_10_new.png)<br/>
   ![CANalyzer 02](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_02.PNG)<br/>
   ![CANalyzer 03](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_03.PNG)
2. Add database <br/>
   ![CANalyzer 11](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_11.png)<br/>
   ![CANalyzer 05](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_05.png)<br/>
   ![CANalyzer 12](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_12.png)
3. Analyze data <br/>
   ![CANalyzer 07](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_07.png)<br/>
   ![CANalyzer 08](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_08.png)<br/>
   ![CANalyzer 13](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/CANalyzer_13.png)

The above is just a basic application of CANalyzer, but it's almost enough to be used for an engineer who works on field problem solving.

### CAN Communication

#### Channels

There are 3 channels on the vehicle:

- Traction CAN
- Charge CAN
- BMS debug CAN

#### Terminal Resister

Terminal resistors are needed in CAN bus systems because CAN communication flows are two-way. The termination at each end absorbs the CAN signal energy, ensuring that this is not reflected from the cable ends.

On our vehicle, these two terminal resistor is designed at BMS and dashboard. <br/>

![CAN bus](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210415094020.png)

However, on the dashboard side, the resistor is controlled by a switch, it means the resistance was effect only when the vehicle is on. Therefore the correct way to check the resistor is turn off the vehicle and measure if the CAN bus resistance is 120 ohm.

#### Signal Characteristic

If you connect channel A to CAN high and channel B to CAN low and use a common reference ground, the standard signal wave should be as follows: <br/>

![CAN signal](https://raw.githubusercontent.com/CarloHan/pic-blog/master/pictures/20210415111518.jpg)

CAN high around +1V and CAN low around -1V. If there is other different wave, the CAN bus must has electric problem, such as CAN high and CAN low opposite, short circuit, or the CAN transceiver was broken and so on. 

### CAN Message 0x2E0 and 0x600

- 0x2E0 named BMS_ERROR, it includes the error signals from BMS
- 0x600 named LMU_FAULT_STS, it includes the error signals from LMU and INVERTER
- Each signal has two states: 0 | 1

### Fault Lists

<div class="admonition tldr">
  <p class="admonition-title">ID 0x600 LMU_FAULT_STS</p>

| ID 0x600| LMU_FAULT_STS |
| -------- | -------|
| LMU_FLT_00 | CAN bus is off.|
| LMU_FLT_01 | LMU found an incoherence between throttle pedal position and switch.    |
| LMU_FLT_02 | LMU senses both shift lever analogue inputs high at the same time.     |
| LMU_FLT_03 | LMU lost communication with battery pack.             |
| LMU_FLT_04 | LMU lost communication with traction inverter.       |
| LMU_FLT_05 | LMU low supply voltage.              |
| LMU_FLT_06 | LMU high supply voltage.           |
| LMU_FLT_07 | LMU temperature is too high.         |
| LMU_FLT_08 | ADC module failure has been detected in LMU.           |
| LMU_FLT_09 | IO module has detected a failure on digital input or output.         |
| LMU_FLT_10 | PLL module failure.                           |
| LMU_FLT_11 | Error during EEPROM reading.              |
| LMU_FLT_12 | Error during EEPROM writing.             |
| LMU_FLT_13 | LMU detected an HV battery over-current.     |
| LMU_FLT_14 | Brake hydraulic circuit pressure too low.           |
| LMU_FLT_15 | Inverter temperature exceeded 85°C and inverter is gradually reducing output power. |
| LMU_FLT_16 | DC link voltage went above high voltage cutback threshold (170 V).        |
| LMU_FLT_17 | DC link voltage went below low voltage cutback threshold (120 V).     |
| LMU_FLT_18 | Inverter operated in slight over-current for a too long time. Controller limits electric drive to rated power.              |
| LMU_FLT_19 | Motor reached 155°C.Controller reduces power to 60%.        |
| LMU_FLT_20 | Invert power up diagnosis fault. Electric drive is allowed to run at reduced power.    |
| LMU_FLT_21 | Inverter has reached 95°C and electric drive has entered thermal protection status.    |
| LMU_FLT_22 | Inverter detected motor stall: phase current exceeded blocked rotor current and motor speed is below 20 rpm for a too long time.             |
| LMU_FLT_23 | CAN communication fault detected. Sending data is not possible.    |
| LMU_FLT_24 | Inverter detected unbalanced 3-phase load.                 |
| LMU_FLT_25 | Motor speed overcome 105% of maximum allowed speed.         |
| LMU_FLT_26 | Motor exceeded 170°C and electric drive entered thermal protection status.    |
| LMU_FLT_27 | Damages to some IGBT/MOS has been detected by HW.     |
| LMU_FLT_28 | DC link voltage overcome fault threshold (180 V).    |
| LMU_FLT_29 | DC link voltage went below fault threshold (110 V).         |
| LMU_FLT_30 | Inverter HW over-current.       |
| LMU_FLT_31 | Motor exceeded 110% of maximum allowed speed.   |
| LMU_FLT_32 | Inverter control logic is too low.      |
| LMU_FLT_33 | Inverter measured abnormal voltage on motor phases neutral point.     |
| LMU_FLT_34 | Resolver value is erroneous.             |
| LMU_FLT_35 | Measured capacitor voltage has exceeded controller maximum.        |
| LMU_FLT_36 | 1) MOSFET / IGBT s/c detection on U phase bottom devices <br/> 2) MOSFET / IGBT s/c detection on V phase  bottom devices <br/> 3) MOSFET  IGBT s/c detection on W phase  bottom devices |
| LMU_FLT_37 | 1) MOSFET / IGBT s/c detection on U phase top devices <br/> 2) MOSFET / IGBT s/c detection on V phase top devices <br/> 3) MOSFET / IGBT s/c detection on W phase top devices     |
| LMU_FLT_38 | Inverter detected a severe fail during power up preventing operation.     |
| LMU_FLT_39 | Motor phase current exceeded imposed SW threshold.      |
| LMU_FLT_40 | Instantaneous motor current overcome HW defined threshold.      |
| LMU_FLT_41 | CAN bus is in warning or error state.        |
| LMU_FLT_42 | A mismatch between application and calibration version has been detected.   |
| LMU_FLT_43 | Calibration section checksum is not correct. Memory corruption is supposed.      |
| LMU_FLT_44 | CAN message overrun.    |
| LMU_FLT_45 | LMU temperature is too low.        |
| LMU_FLT_46 | Software task overrun.      |
| LMU_FLT_47 | Interrupt vector section checksum is not correct. Memory corruption is supposed.  |
| LMU_FLT_48 | Application section checksum is not correct. Memory corruption is supposed.     |
| LMU_FLT_49 | Pointer to application pointing in a non application sector.          |
</div>

<div class="admonition tldr">
  <p class="admonition-title">ID 0x2E0 BMS_ERROR</p>

| ID 0x2E0                         | BMS_ERROR                                                   |
| ------------------------------- | ----------------------------------------------------------- |
| ErrCellUndervoltage             | BMS detected a cell under voltage error                     |
| ErrCellOvervoltage              | BMS detected a cell over voltage error                      |
| ErrCellDiffOutRng               | BMS detected a cell voltage difference exceed range error   |
| ErrCellOvertemperature          | BMS detected a cell over temperature error                  |
| ErrCellUndertemperature         | BMS detected a cell under temperature error                 |
| ErrPrechargeError               | BMS detected the pre-charge failure error                   |
| ErrHvNegContactorError          | BMS detected the negative contactor error                   |
| ErrHvPosContactorError          | BMS detected the positive contactor error                   |
| ErrOvercurrent                  | BMS detected over current error                             |
| ErrCanCurrentSenslost           | /                                                           |
| ErrGssGndError                  | /                                                           |
| ErrGssVccError                  | /                                                           |
| ErrHvSwitchedOutOverCurr        | /                                                           |
| ErrHvBusNoVoltage               | /                                                           |
| ErrEepromReadError              | /                                                           |
| ErrEepromWriteError             | /                                                           |
| ErrBmtMrPrechargeContactorError | /                                                           |
| ErrBmtMrHvPosContactorError     | /                                                           |
| ErrSlaveModuleConLost           | /                                                           |
| ErrDcDcNotWorking               | /                                                           |
| WrnCellUndervoltage             | BMS detected a cell under voltage warning                   |
| WrnCellOvervoltage              | BMS detected a cell over voltage warning                    |
| WrnCellDiffOutRng               | BMS detected a cell voltage difference exceed range warning |
| WrnCellOvertemperature          | BMS detected a cell over temperature warning                |
| WrnCellUndertemperature         | BMS detected a cell under temperature warning               |
| WrnOvercurrent                  | BMS detected over current warning                           |
</div>

---

> Company: MECAPROM
> Author: YING.H
> Date: 15/04/2021
> Version: 1.1
> Changelog: V1.1 Add PicoScope and CAN bus checking
