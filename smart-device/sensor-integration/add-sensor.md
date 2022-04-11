---
layout: default
title: Add Sensor
parent: Sensor Integration
grand_parent: Smart Device
---

# How to Add a Sensor

Things to consider for adding sensors.

1. <span style="color:#7253ed;font-weight: bold;">Calibration</span>
	- The analogRead returns the voltage which has to be calculated to the appropriate reading.
	- The equation to use: 
		input: voltage
		output: appropriate units
	- In the calibration step, the value of the output is given. 
	- The constant can be calculated which will be unused in future readings. 

2. <span style="color:#7253ed;font-weight: bold;">Testing</span>
	- The testing we have currently done was using Arduino UNO for the same sensor. 
	- The assumption is that we have UNO library for the same sensor and confirm the reading and voltage.

3. <span style="color:#7253ed;font-weight: bold;">Resolution of voltage reading</span>
	- When testing values against Arduino UNO, there is difference in mapping of input voltages
		Arduino Uno: 10-bit converter (return values( 0~5 volts / 1024 units ))
		Arduino Zero: 12-bit ADC capabilities (return values ( 0 ~ 3.3 volts/ 4095 units))

4. <span style="color:#7253ed;font-weight: bold;">Example</span>
	- Electric Conductivity Sensors (DFRobot)
	1. Equation
		kValue = RES2 * ECREF * compECsolution / 1000 / voltage 
		- Source: DFRobot Library froc EC sensor
		- RES2: 820
		- ECREF: 200
		- compECsolution: from the buffer solution
		- voltage: reading coming in the zero
	2. Testing
		- Testing was done to compare the readings coming from Arduino Uno, and Arduino Zero.

This section provides an overview of how to add a defined sensor to the smart device.
{: .fs-6 .fw-300 }
