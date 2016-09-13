---
layout: page
title: Lab 5 - Analog In
permalink: /lab-5/
---

# **Lab Objectives:**

+ 

# **Lab 5 Resources:**

+ [Analog Input Video](https://vimeo.com/86551311#t=0m56s)
+ Adafruit's guide to [Forse Sensitive Resistors (FSR)](https://learn.adafruit.com/force-sensitive-resistor-fsr)

# **Digital Input and Output Lab:**

**For this lab you will need the following parts:**

+ Solderless Breadboard and hookup wire
+ Arduino microcontroller module & USB connector
+ LEDs of different colors
+ 560 ohm (or anything from 220 to 1K) and 10 Kilohm resistors
+ 10Kohm potentiometer
+ Force-sensing Resistors (or a different for of variable resistor)

**Setup the breadboard** - Connect a potentiometer to analog in pin 0 of the module, and an LED and a resistor to digital pin 9:

<br>
![Lab 5 Schematic - Analog Input](/object-fall-16/assets/lab5-01.png)
<br><br>

**Program the Module**

First, establish some global variables: one to hold the value returned by the potentiometer, and another to hold the brightness value. Make a global constant to give the LED’s pin number a name.

	const int ledPin = 9;       // pin that the LED is attached to
	int analogValue = 0;        // value read from the pot
	int brightness = 0;         // PWM pin that the LED is on. 

In the setup() method, initialize serial communications at 9600 bits per second, and set the LED’s pin to be an output.

	void setup() {
	    // initialize serial communications at 9600 bps:
	    Serial.begin(9600);
	    // declare the led pin as an output:
	    pinMode(ledPin, OUTPUT);
	}

In the main loop, read the analog value using analogRead() and put the result into the variable that holds the analog value. Then divide the analog value by 4 to get it into a range from 0 to 255. Then use the analogWrite() command to face the LED. Then print out the brightness value.

	void loop() {
	    analogValue = analogRead(A0);    // read the pot value
	    brightness = analogValue /4;       //divide by 4 to fit in a byte
	    analogWrite(ledPin, brightness);   // PWM the LED with the brightness value
	    Serial.println(brightness);        // print the brightness value back to the serial monitor
	}

When you run this code, the LED should dim up and down as you turn the pot, and the brightness value should show up in the serial monitor.

# **Other Variable Resistors** (going a bit further...)
