---
layout: default
title: MEMS Gas Sensors - MiCS-5524 (Breakout)  
parent: Fermion
grand_parent: Sensors
permalink: /docs/sensors/fermion/MEMS-gas-sensor-MiCS-5524/
---

1. TOC
{:toc}

---

## Introduction
This a hydrogen and nitrogen oxide gas concentration sensor launched by DFRobot.

The sensor uses MEMS technology to support gas concentration detection of CO, CH4, C2H5OH, C3H8, C4H10, H2, H2S and NH3. The matching sample code integrates the concentration conversion formula of various gas to facilitate the testing and use of sensors.

The product supports 5V power supply, analog voltage output, and has power supply enable/disable pins for low power consumption.

## Features
Support a variety of harmful gas detection
Integrate the calculation formulas of various gas concentration
Low power consumption
I2C digital output
Compatible with the 3.3~5.5V master controller

## Applications
Gas leak detection
Gas safety equipment
Air environment detection

## Specifications
Detection of Physical Quantities: Gas concentration or gas leakage of CO, CH4, 2H5OH, C3H8, C4H10, H2, H2S, NH3

Operating voltage: 4.9～5.1V DC

Power dissipation: 0.45W

Output signal: Analog quantity

Measuring range:
         1 – 1000ppm (Carbon monoxide CO)
         10 – 500ppm (Ethanol C2H5OH)
         1 – 1000ppm (Hydrogen H2)
         1 – 500ppm (Ammonia NH3)
         >1000ppm (Methane CH4)

Working temperature: -30～85℃

Working humidity: 5～95%RH (No condensation)

Storage temperature: -40~85℃

Lifespan: >2 years (in the air)

Circuit board size：12mm x 16mm

Mounting hole size：Inner diameter 2mm/ outer diameter 4mm

## Documents
Product wiki (https://wiki.dfrobot.com/Fermion__MEMS_Gas_Sensor___MiCS-5524_SKU_SEN0440)

MiCS-5524 Datasheet (https://img.dfrobot.com.cn/wiki/5b973267c87e6f19943ab3ad/86011e31a53db4f1bb6a3978de97a135.pdf)

Schematics Diagram (https://dfimg.dfrobot.com/nobody/wiki/bc7b994d37fdaffc6e43624bda91cbde.pdf)

Dimension and Component Layout (https://dfimg.dfrobot.com/nobody/wiki/065f0240e12ab11e527c4c6cf91799ba.pdf)

---

## JSON 
Publish Topic: device/reading/sensor/ch4
<div class="code-example" markdown="1">

```json
{
  value:        # float
}
```
</div>

Subscribe Topic: device/config/sensor/ch4
<div class="code-example" markdown="1">

```json
{
  state:          # binary
}
```
</div>