---
layout: post
title:  "Project - The Internet Of Holiday Lights"
description: "Using Technology to connect our holiday lights to the Internet."
image: assets/images/iotholiday/splash.jpg
featured: true
author: ipv1
categories:
  - Project
tags:
  - Arduino
  - Raspberry Pi
  - Lights
  - Linux
  - OpenHAB

---

Using Technology to connect our holiday lights to the Internet.

## ABSTRACT

At the end of 2014, Infineon, MCM electronics and Element14, sponsored a IoT Holiday Lights challenge where 20 people were asked to use an Infineon RGB LED Shield, Arduino Yun and an Arduino Uno in a Holiday lights project that utilised the connectivity to the internet. We designed a Living Room lights setup in our own living room to create an extravaganza of lights which were controlled by music as well as the user’s commands. OpenHAB was employed to be the Front end for the control panel which could be accessed by a mobile device over the network. The final result was demonstrated using the video shown below and we won the first prize which was a CelRobox which is a 3D printer.


## INTRODUCTION

The holidays mean different things to different people. To kids it means gifts, to teens it means time off, to the professional its a time to be away from the stress of daily life, to the mother it means a display of culinary skill and to the elderly it means a time when lots of people visit. Whatever may be means, the end result is a fun time and sharing of happiness.
My project for the Internet of Holiday lights was based around our living room which was not very livable. It was a mess and with the upcoming holidays I wanted to set the living room in such a way that it would be suitable for entertaining guests. Additionally I wanted to accomplish the above mentioned in such a way that the holiday lighting becomes part of the living room and I don’t need to remove it after the holidays. Hence the concept of Dynamic Living-room Lighting.

![alt text](/assets/images/iotholiday/1.jpg "Voltage Divider"){: .align-center}

## THE CONCEPT

The original concept of the project came from the fact that we have a very disorganized living room. Element14, Infineon and MCM Electronics sponsored some parts and I wanted to make them the hero of this project. Additionally iot.Eclipse.org provided some pretty nifty tools to work from. I started by drafting an idea around the Infineon RGB LED Shield and the fact that the YUN has the capability to connect to a Wi-Fi Network. Being an Electrical Engineer I am not an expert on software development and GUIs and hence I took to something that I understand which is OpenHAB. The design was drafted and the first few blogs were published around a focused plan. The target was not only to build the electronics but to demonstrate how practically the things fit into real life. And thus I began one module at a time.

![alt text](/assets/images/iotholiday/2.jpg){: .align-center}

## THE IMPLEMENTATION

Hence I began working with the YUN and the Infineon RGB LED Shield and in the process I did a review and to make life easier, I wrote a library for the shield. In order to control the YUN, I used Benjamin Cabe sir’s original code and added my own twist to it so that it can received the data in a predefined format. I added some basic Low Pass Filter and connected the audio to the system and made the lights dance to the music. The lights were meant for the living room and hence me and my wife moved to make the Living Room more usable. A DIY frame later, the LEDs were up above the curtains and I hooked them up for the final build. For the interface, I used OpenHAB to make things pretty for the user. The code is similar to Javascript without the HTML to present it and presented it to the world.

![alt text](/assets/images/iotholiday/3.jpg){: .align-center}

![alt text](/assets/images/iotholiday/4.jpg){: .align-center}

With the Lights functional, I moved on to create the tree which used up another arduino and the communication was established over a wire. I used RGB LEDs that can be chained together and 120 LEDs on the tree make for some pretty bright lights. I wrote the code for the Tree which I explained in my last blog and the whole thing lit up like… christmas! The tree can light up according to music or a fixed color by Software or in predefined patterns.

![alt text](/assets/images/iotholiday/5.jpg){: .align-center}

![alt text](/assets/images/iotholiday/6.jpg){: .align-center}

The lights and sound needed some dance. My wife and I made minions(pun intended) and I used some element14 boxes to make a crank-piston arrangement and added a motor. This made the minions dance and I wrote a blog post about it so that anyone can make it at home. Moving on, I added a raspberry Pi to the mix since my YUN was busy behind the curtains(literally). A python script later, I was able to read tweets mentions and hashtags and I used it to trigger a minion Dance whenever someone mentioned @ip_v1 on twitter with #happynewyear or #HappyChristmas. It is so much fun and there is a blog post about that as well. I also added a little MQTT to it so that I could control the minions using OpenHAB and now they sing and dance on queue.

![alt text](/assets/images/iotholiday/7.jpg){: .align-center}

![alt text](/assets/images/iotholiday/8.jpg){: .align-center}

The final build was completed, cleaned and documented. A fireplace was fabriacated out of styrofoam and a wooden shelf was converted into a snowy scene for the minions to stand. The shelf lights are controlled via IR Control and added ambiance to the shelf. The completed system is demonstrated in a 10minute video below.

![alt text](/assets/images/iotholiday/9.jpg){: .align-center}

![alt text](/assets/images/iotholiday/10.jpg){: .align-center}

## THE DEMONSTRATION

I made the video with the help of my wife and it was the first time I actually edited a video which made it a long learning process. The end result is given below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/-ZqZz6i7-mw" frameborder="0" allowfullscreen></iframe>

## CONCLUSION

It was fun. I had planned on finishing the project before the holidays but I ended up doing a lot more tweaking and the final system is something that will stay in the living room as a permanent resident. The tree will also be a permanent resident as well and everytime someone asks why, we can demonstrate the system and christmas will never actually be over. I have tried to put up as much detail as possible and hope that next year someone will take a piece of this project to their living room and sends me a tweet and makes the minions sing and dance.

Thank you,

Inderpreet Singh
