---
layout: page
title: Lab 7
permalink: /lab-7/
---

# **Lab Objectives:**

+ Control a stepper motor using an h-bridge
+ Program the stepper to sweep back and forth
+ Add an input to control the stepper output

# **Lab 6 Resources:**

+ [Meet the Motors (video)](https://vimeo.com/84274150)
+ [Stepper Motors (video)](https://vimeo.com/101362995)
+ [Tom Igoe's Notes on Steppers](http://www.tigoe.net/pcomp/code/circuits/motors/stepper-motors/)
+ [Stepper Speed Control](https://www.arduino.cc/en/Tutorial/StepperSpeedControl)

<br>
<hr>

# How your H-bridge works

The L293NE/SN754410 is a very basic H-bridge. It has two bridges, one on the left side of the chip and one on the right, and can control 2 motors. It can drive up to 1 amp of current, and operate between 4.5V and 36V. 

*The H-bridge has the following pins and features:*

+ Pin 1 (1,2EN) enables and disables our motor whether it is give HIGH or LOW
+ Pin 2 (1A) is a logic pin for our motor (input is either HIGH or LOW)
+ Pin 3 (1Y) is for one of the motor terminals
+ Pin 4-5 are for ground
+ Pin 6 (2Y) is for the other motor terminal
+ Pin 7 (2A) is a logic pin for our motor (input is either HIGH or LOW)
+ Pin 8 (VCC2) is the power supply for our motor, this should be given the rated voltage of your motor
+ Pin 9-11 are unconnected as you are only using one motor in this lab
+ Pin 12-13 are for ground
+ Pin 14-15 are unconnected
+ Pin 16 (VCC1) is connected to 5V

Below is a diagram of the H-bridge and which pins do what in our example. Included with the diagram is a truth table indicating how the motor will function according to the state of the logic pins (which are set by our Arduino).

<br>
![H-Bridge Pinout](/object-fall-16/assets/h-bridge.jpg)
<br><br><br>

For this lab, both enable pins are connected to 5V to keep them HIGH all the time so the bridge is constantly enabled. The motor logic pins also connected to designated digital pins on your Arduino so you can send them HIGH and LOW control the stepper. The motor supply voltage connects to the voltage source for the motor, an external 12V DC power supply. **Not all steppers run on 12V, but the one used for this example does. Check your stepper’s ratings before you power the H-bridge.**

# How the stepper motor works

The stepper motor has two coils to control it. Each coil has a center connection as well, and the center connections are joined together, which is what makes this a **unipolar stepper**. If you don’t connect the center connection, then the motor will work very much like a **bipolar stepper**, each coil operating independently. This is how you’ll use it for this exercise. Each coil will connect to one side of the H-bridge. The pink and orange wires (the first coil) will connect to one side of the bridge, while the yellow and blue wires (the other coil) connect to the other side of the bridge.

<br>
![Stepper Motor](/object-fall-16/assets/lab7-03.png){:height="360px" width="400px"}
<br><br><br>

<br>
<hr>

# **Part 1: Controlling a Stepper Motor With an H-Bridge**

**Supplies**

+ Solderless Breadboard and hookup wire
+ Arduino microcontroller module & USB connector
+ Stepper motor
+ L293NE or SN754410 H-bridge
+ 12V DC power supply
+ DC power jack

**Setup the Circuit**

Connect the H-bridge as shown below:

<br>
![H-Bridge Schematic](/object-fall-16/assets/lab7-01.png){:width="550px"}
<br><br><br>

Next, connect the motor to the h-bridge:

<br>
![H-Bridge Schematic](/object-fall-16/assets/lab7-02.png)
<br><br>

***Note that the H-bridge’s DC power is coming from the 12V DC connector. It shares a common ground with the Arduino, though.***

<br>

Lastly, connect the H-Bridge to the microcontroller.

The H bridge’s control inputs are connected to the microcontroller’s input pins digital 8 through 11 as follows:



<br>
![H-Bridge Schematic](/object-fall-16/assets/lab7-04.png)
<br>

<br>


If you are stuck building the circuit, you can check [this graphic](/object-fall-16/assets/lab7-fritz.png) to double check your connections.

<br>

**Program the microcontroller**

Program the microcontroller to run the stepper motor through the H-bridge using the stepper library. For your first program, it’s a good idea to run the stepper one step at a time, to see that all the wires are connected correctly. If they are, the stepper will step one step forward at a time, every half second, using the code below:

	#include <Stepper.h>
 
	const int stepsPerRevolution = 512;  // change this to fit the number of steps per revolution
	                                     // for your motor
	 
	// initialize the stepper library on pins 8 through 11:
	Stepper myStepper(stepsPerRevolution, 8,9,10,11);            
	 
	int stepCount = 0;         // number of steps the motor has taken
	 
	void setup() {
	  // initialize the serial port:
	  Serial.begin(9600);
	}
	 
	void loop() {
	  // step one step:
	  myStepper.step(1);
	  Serial.print("steps:" );
	  Serial.println(stepCount);
	  stepCount++;
	  delay(500);
	}

Once you’ve got that working, try making the stepper move one whole revolution at a time. The number of steps per revolution will depend on your individual stepper, so check the data sheet for the number of steps per revolution.

***For your documentation, I want to see a video of the stepper turning one full rotation forward, then one full rotation backward, then forward again, then backward again, etc..***


<!-- #include <Stepper.h>
 
const int stepsPerRevolution = 512;  // change this to fit the number of steps per revolution
                                     // for your motor
 
// initialize the stepper library on pins 8 through 11:
Stepper myStepper(stepsPerRevolution, 8,9,10,11);            
 
void setup() {
  // set the speed at 60 rpm:
  myStepper.setSpeed(10);
  // initialize the serial port:
  Serial.begin(9600);
}
 
void loop() {
  // step one revolution  in one direction:
   Serial.println("clockwise");
  myStepper.step(stepsPerRevolution);
  delay(500);
 
   // step one revolution in the other direction:
  Serial.println("counterclockwise");
  myStepper.step(-stepsPerRevolution);
  delay(500);
} -->


With a high-step-count stepper, you may need to change the speed. If the motor steps are run too fast, the motor coils don’t have a chance to energize and de-energize in order to step the motor.

<br>
<hr>

# **Part 2: Add An Input to Control the Stepper**

Choose any analog input to add to your circuit. Program your microcontroller such that the analog input controls the motor. Get creative!

<br>
<hr>

<br>

# **Lab 7 is due before class on Tuesday October 11th** 

Your blog response should include a *clear* video of your working circuit and a brief description of what you made. Submit a link to your blog post on Edmodo. 



