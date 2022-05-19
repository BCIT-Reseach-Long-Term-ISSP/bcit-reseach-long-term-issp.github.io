---
layout: default
title: Atlas EZO Electrical Conductivity Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/atlas-ezo-electrical-conductivity-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# Atlas EZO Electrical Conductivity Sensor Calibration

A walkthrough of the Atlas EZO Electrical Conductivity Sensor calibration procedure
{: .fs-6 .fw-300 }

## Materials

To be filled in

## Procedure Bare Metal Arduino Zero

Same procedure as the procedure for an Arduino Uno.

## Procedure Arduino Uno

1. Grab an Arduino Uno

2. Plug in the sensor into the Arduin Uno

  A) Sensor chip's VCC pin to the 3.3V pin on the Arduino

  B) Sensor chip's GND to a GND pin on the Arduino

  C) Sensor chip's RX pin to this Arduino's TX pin, determined by the above code, in this case digital pin 9
  
  D) Sensor chip's TX pin to this Arduino's RX pin, determined by the above code, in this case digital pin 8

3. Flash the following program to the Arduino Uno using the Arduino IDE


```c++
#include <SoftwareSerial.h>
#define rxPin 8
#define txPin 9

SoftwareSerial mySerial(8, 9); 

void setup() {
  Serial.begin(9600);
  while (!Serial) {
  }
  Serial.println("UART Communication Program for Working with Sensors");
  mySerial.begin(9600);
}

void loop() { 
  if (mySerial.available()) {
    Serial.write(mySerial.read());
  }
  if (Serial.available()) {
    mySerial.write(Serial.read());
  }
}
```

4. The software serial library should come pre-installed, but if it does not, install it.

5. Open the Serial Monitor

6. If you start seeing measurements value coming into the serial monitor, the sensor is connected correctly.

7. If you do not see anything in the serial monitor, type in "i" into the serial monitor and press enter.

You should see a response on the serial monitor, this means that sensor is properly connected.

8. Once properly connected, if you don't see measurements constantly coming into the serial monitor, type in "C,1" into the serial monitor and press enter.

9. Disable all paramaters for meaurements, ref page 35

10. Enable the EC measurement, ref page 35

11. Follow the remaining calibration instructions from the formal documentation, starting at page 12: https://files.atlas-scientific.com/EC_EZO_Datasheet.pdf

12. After calibration is complete, type in "C,0" into the serial monitor and press enter.

This will stop the sensor from sending continuous measurements.

13. Calibration is now complete
