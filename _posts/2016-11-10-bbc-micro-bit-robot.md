---
title:  "BBC Micro Bit based Line Follower Robot"
excerpt: “An introduction to the BBC microbit and a tutorial on making a line following robot"
header:
  image: /assets/images/unsplash-image-2.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Project
tags:
  - Linux
  - OpenHAB
  - Edison
---

## INTRODUCTION

The BBC Microbit is a small ARM based, user friendly, micro controller targeted towards computer education in the UK. It has been developed by the partnership of a long list of organisations including Microsoft, Element14, Nordic, NXP and many more. 

{% include base_path %}

{% include toc title="Contents" %}

The intended audience is school children and there are four official ways to write programs for the BBC Micro Bit. They are.

* CodeKingdoms, using JavaScript;
* Microsoft Block Editor, based on Blockly;
* Microsoft TouchDevelop;
* MicroPython.

In addition to these, it is possible to really go deep with mBed at mbed.org for access to the underlying runtime and system code. For the most part, the TouchDevelop Editor from Microsoft is a good balance between programming language and user friendly IDE.

Element14 was kind enough to provide me with one of these boards and I though I would do something with the board beyond the blinking LED. So the simplest mechanical project I could think of was a simple line follower robot. The objective is to have a machine follow a line- thats it! First, I start with introducing the BBC Micro bit and then making a small circuit that can be used to detect a black line on a white flat sheet. This is accomplished using some IR LEDs and photodiodes.

We go on ahead and write a small piece of code to read the sensors and then display the movement direction on the matrix display. Here is the video for a more in detail lesson.

<iframe width="560" height="315" src="https://www.youtube.com/embed/7qnSsc54bEQ" frameborder="0" allowfullscreen></iframe>

Next, we go through the concept of a motor driver, the basic circuit and controlling DC motors with the BBC microbit. We then move to add the motors to a chassis and then write the basic routine to make the robot follow a simple line.
Here is a video tutorial and demo video for the project part 2

<iframe width="560" height="315" src="https://www.youtube.com/embed/lhRkDi4RNN4" frameborder="0" allowfullscreen></iframe>


## The Motor Driver

The L293D is a dedicated motor driving chip with 4 half H-bridges or two full H-Bridges which can be employed to control the direction two connected motors. You may choose to make an H-Bridge using transistors or even MOSFETs on a strip board etc but the single chip solution is simpler and quicker. The pin diagram and connection diagram for the L293D is shown below.

![alt text](/assets/images/microbit/1.jpg){: .align-center}

The GPIOs in the BBC Micro:bit can be used to set the speed and direction of the motors however for this exercise, we will only be interested in modifying the direction of the motors. Since the GPIOs available on the breakout board also include the ones used for onboard peripherals such as the matrix display, we must select the ones that are unused. Take a look at the pinout diagram below. We need four IOs out of which two are used for direction and two are used for speed or turning the motors ON and OFF.

![alt text](/assets/images/microbit/2.png){: .align-center}

## FORMING A CHASSIS

After connecting the motor driver and motors, we need to put everything together along with a chassis, wheels and our sensor board. I have made a simple chassis, but you can create something more elaborate and used different parts according to preference. The sky is the limit. Add batteries and we are good.
WRITE THE PROGRAM

We will continue using touch develop to make the program and i order to make the decision to turn right or left or move straight, we will add an IF-THEN-ELSE ladder within the loop we created the last time. The program can be downloaded as a file using the link provided at the bottom of this page. Compile the code and upload the hex file to the BBC Micro:bit.
CREATE A TRACK AND TEST

In order to follow a line, we need a line for which we use some black water colours and a white paper sheet. Draw a simple circle initially to test out the functionality. Make sure that the line is not too thick else the sensor will have problems detecting turns and will get stuck easily. We just need the line to thick enough that it is detected by each of the sensors individually.
Test her out.
Let me know what you think in the comments section and give a like and subscribe to the youtube channel for more.

Happy hacking.
