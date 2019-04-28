---
title:  "Project - Low Cost Connected Christmas"
excerpt: "The dollar-store inspired Christmas project"
header:
  image: /assets/images/dollar_christmas/splash.jpg
  caption: "Music and connectivity on a budget"

image: /assets/images/dollar_christmas/splash.jpg
categories:
  - Project
tags:
  - Arduino
  - Raspberry Pi
  - Lights
  - Linux
  - Bluetooth
toc: true
toc_label: "Table Of Contents"
toc_icon: "book-open"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## ABSTRACT

Christmas is a very special time of year for me and my family. Every  year, we celebrate the holidays by making a project together and it  becomes a memory for me and my wife.

Having  moved across the continent, this year's project is one that is on a  budget. I started by procuring items from the dollar store and with a  handful of components that I brought with me, my wife, my son and I set  out to build a mini Christmas festival. I will be keeping the  explanation brief though the discussion can be a lengthy one.

Our  project consists of 2 parts which are intended to serve two different  purposes. The first part is designed with the Raspberry Pi at the centre  and Texas Instruments BLE lights as the end devices along with a sense  hat for good measure. Python based web app allows for the control of  colours for the budget tree as well as the jolly snowman.

The  second part employs two BBC:Micro bits talking to each other wirelessly and are allow for the control of a string of lights and a musical house.

Take a look at the video and then we can walk through the construction.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/FL8XDP5LaUE" frameborder="0" allowfullscreen></iframe>

## The Python Server

The  Texas Instruments BLE lights can be connected to via a number of  methods. I wrote about talking to them via NodeJS over at HackADay  making them IoT Lights and wanted to challenge myself to use python  instead.

Here is a basic block diagram of the plan.

 

[![img](https://www.element14.com/community/servlet/JiveServlet/downloadImage/38-31425-659276/IMG_20190112_065130235.jpg)](https://www.element14.com/community/servlet/JiveServlet/showImage/38-31425-659276/IMG_20190112_065130235.jpg)

 

### Working

The Raspberry Pi 3 runs a Python Flask Server that does two things.

1. It serves up html/css/js files that are requested by a web browser. The  loaded page contains a GUI with coloraturas pickers as well as action  buttons. The page is also loaded with a javascript element that allows  coloraturas picker data to be sent via simple REST like call to the  python server.

 

2. The Flask server also exposes a REST like API that allows a client to select a light and send it coloraturas data

Once  the web page is loaded, the user can use a coloraturas picker for a  particular light. Once the user make a selection, a REST call is trigged  and the RGB data is sent to the Flask server. This is translated from  text to hex values and passed onto the Bluetooth LE module.

The  Bluetooth LE module is also written in python and allows for the  scanning and then communication with BLE lights. The UUIDs are made part  of the module and hence once the RGB values are passed to it, it scans  for BLE light presence. If found, it then updates the BLE light's  characteristics thereby changing the light.

There  are a number of components to this and the code is flexible enough to  allow future expansion. I also added an animation function that sends  varying RGB data to the lights making them change colour in sync with  each other.

### Dollar stuff

Both  the tree and snowman are dollar store bought outs and I implanted the  LED lights to make things work. Neo-Pixel strip are way too expensive  for us right now and would also require an external power source. I did  get an RGB LED strip from Peter Sir but buying an SMPS, LED driver, PCB  etc etc was not in my budget this year.

## BBC Micro bit remotes

My  son is almost three and he loves to play around with machines and  buttons. I wanted to give him the ability to interact with the Christmas  project and hence I opted for the wireless control.

### Working

 One  of the Microbits have the pins broken out and I used 2N3904 NPN  Transistors as switched to turn ON and OFF two things. First was an LED  strip which was procured at the dollar store and the LEDs change colour  due to their internal circuitry.

[![img](https://www.element14.com/community/servlet/JiveServlet/downloadImage/38-31425-659259/IMG_6104.jpg)](https://www.element14.com/community/servlet/JiveServlet/showImage/38-31425-659259/IMG_6104.jpg)

 

Second,  is a small house with a music chip that plays the Christmas carols  which was perfect. After hacking it open, I connected the transistor and  resistor directly to the contact.

The code sends commands to toggle the GPIOs ON and OFF and the state is saved within the remote itself.

 I also employ the LED matrix to display a merry Xmas once the microbit is glued atop the small house.

One button allows for toggling the lights while the other button allows for control over the music (and message board).

I could have easily connected the Microbit to the Raspberry Pi by the use of GPIOs.

## Model Construction (on a budget)

Water  colours can and will bring out the child in everyone and my better half  was more than happy to create a model. Cotton for snow and just paint  and crayons made this project a family effort. After all its all about  bringing everyone together.


[![img](https://www.element14.com/community/servlet/JiveServlet/downloadImage/38-31425-659260/IMG_20190112_032737407.jpg)](https://www.element14.com/community/servlet/JiveServlet/showImage/38-31425-659260/IMG_20190112_032737407.jpg)


Some  Christmas toothpicks and ornaments later, we had a small village with  Santa Clause, reindeers and a cottage. My son added his collection of  Paw Patrol pups and I added a Lego Anakin Skywalker with R2D2. Everyone  had a lot of fun

## The code

 Yes  the entire code is up on GitHub and you can download and modify as you  like. I am learning better python and hence packaging things was  something new.

 Head on over to [http://github.com/inderpreet/py_e14_holiday_lights_and_music](https://www.element14.com/community/external-link.jspa?url=http%3A%2F%2Fgithub.com%2Finderpreet%2Fpy_e14_holiday_lights_and_music)

 I am yet to do a setup script though manually installing the modules is quite simple.

<script src="https://gist.github.com/inderpreet/cc42817ee0c7f03bc86841ff4b7d016f.js"></script>

 The script for the controller BBC Microbit is as follows.

<script src="https://gist.github.com/inderpreet/70b3833ffe9197fbc5b32c958ea2acbe.js"></script>

## Conclusion

 Christmas  is all about family and I a feel these projects have become a tradition  for us. We did the best we could given the limited resources and budget  I have this year and I am hoping my son will be an active participant  next year. I ventured into Python for this project and learned about  creating a web server as well as implementing a REST API. I also got the  chance to put the BBC Microbit in the hands of my son and I am hoping  this will escalate.

I hope you had as much fun watching and reading as we had making it. Thanks again and belated happy holidays.
