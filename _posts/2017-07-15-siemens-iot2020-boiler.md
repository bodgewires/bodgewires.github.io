---
title:  "Project - IoT Boiler Controller using Siemens IoT 2020"
excerpt: "Creating a Safe Demonstration of an Industrial Boiler Control Using the IoT2020"
header:
  image: /assets/images/iot2020/splash.jpg
  caption: "The IoT Boiler Controller"
categories:
  - Project
tags:
  - Linux
  - Galileo
  - Siemens
  - Arduino
  - Ethernet
  - NodeJs
  - Node-Red
  - Python
  - C++
toc: true
toc_label: "Table Of Contents"
toc_icon: "book-open"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## Description

The IoT Boiler Controller is a mash-up of multiple technologies in an effort to demonstrate competency in designing and developing complex applications.

## Details

### Background

In the April of 2017, RS components and [The Breadboard](https://www.thebreadboard.ca) launched a competition on [Hackster.io](https://www.hackster.io) and challenged us to create a project using the Siemens IoT2020. The theme was industrial automation since the IoT2000 is designed for industrial applications and the sky was the limit. 

My idea was to explore the capabilities of the IoT2020 in terms of the languages it could be programmed in. Since the target audience for the platform is makers who intend to develop an industrial project, it seemed just that all the maker friendly languages be tested out.

For my case study, I chose to work with the following languages.

1. Arduino - For the basic maker
2. Node-Red - For the experience maker
3. NodeJS and Python - For the scripting maker
4. C++ - for the advanced maker

I chose the design of an Industrial Boiler since the "Process Control Scenario" is usually a common template for many real world cases. Additionally it allowed me to experiment with a number of communication protocols and add to the complexity of the design. Finally, I added an IoT Dashboard for remote monitoring over the internet using [Initial State](https://initialstate.com)

Read on for more details on the project.

### The Boiler Design Document - Agile Style

The block diagram below shows the main components of this project. At the heart of the design in the Siemens IoT2020 which is responsible for communicating and controlling all the peripheral devices. The system is designed like any process control scenario with an actuator which in my case is a Pump controlled via Relay and a process sensor portrayed by the Flow Sensor. An additional temperature sensor allows to extend functionality for safety and cut-off demonstrations. 

![Block Diagram](/assets/images/iot2020/block-diag.jpg){: .align-center}

The communication between the gateway and the various components is enabled by protocols such as ModBUS/TLV, MQTT, REST and plain TCP/IP(Sockets).

The system is divided into three sub projects, each with it's own set of stories. All the stories are summarized at the end in an Agile view of the Project.

### Sub-Project 1 - TCP Socket Server, Serial Bridge and ModBUS Edge Device

The requirement is to design and deploy a ModBUS variant where the edge device is an Arduino Clone that communicates over a ModBUS like protocol and controls the Pump. On the gateway side, a software TCP/IP to ModBUS bridge is to be implemented which can accept socket requests and can relay commands received over this socket connection to the ModBUS/Serial line. The architecture diagram for this sub-project is given below.

<figure class="half">
    <img src="/assets/images/iot2020/sub1-arch.jpg">
    <img src="/assets/images/iot2020/sub1-pic.jpg">
    <figcaption>ModBUS Pump Control</figcaption>
</figure>


|  #  | Story Name (Tag)		| Story Description								| Priority 	| Points(est)   |
|:---:|-------------------------|-----------------------------------------------|:---------:|:-------------:|
|  1  | ModBUS Implementation	| Implement TLV/ModBUS like	protocol in Arduino	|1			| 	3			|
|  2  |	Setup IOT2020 IDE 		| Setting up the IDE to work the IOT2020 C++	|2			|   1			|
|  3  | IOT2020 Socket Server	| C++ app for accepting Socket connections		|3			|   2			|
|  4  | IOT2020 ModBUS App 		| C++ app for Serial communication 				|4			|   1			|
|  5  | Python Test Script 		| Test and Fallback Script for Module 			|5			| 1				|

The TCP/IP Client and NodeJS application along with the dashboard are a separate iteration hence excluded from this storyboard.

The hardware part works with an Arduino Clone with an FTDI Chip that connects to the USB port of the IoT2020. This serves as proof of concept that serial enumeration comes pre-built and any serial protocol device can be accommodated into a design. Industrial grade USB to ModBUS converters can be deployed into this design without additional effort.

### Sub-Project 2 - MQTT Sensor Edge Device with NodeJS

The requirement is to design and deploy a sensor device that can connect via Ethernet and the local network. The communication happens over MQTT which is an existing lightweight protocol that sits atop TCP/IP. This allows for better throughput and scalability and is demonstrated via a flow-rate sensor that transmits rate of fluid flow along with temperature data from a remote location. The architecture diagram for this sub-project is given below.

<figure class="half">
    <img src="/assets/images/iot2020/sub2-arch.jpg">
    <img src="/assets/images/iot2020/sub2-pic.jpg">
    <figcaption>ModBUS Pump Control</figcaption>
</figure>


|  #  | Story Name (Tag)		| Story Description								| Priority 	| Points(est)   |
|:---:|-------------------------|-----------------------------------------------|:---------:|:-------------:|
|  1  | Arduino Implementation	| Implement MQTT sensor data transmission		|1			| 	1			|
|  2  |	Node-RED Setup	 		| Setting up the NodeRED to work the IOT2020	|2			|   1			|
|  3  | Node-RED Flows and Dash	| Implementation of the Node-RED Flows and Dash	|3			|   2			|
|  4  | Initial State Integ.	| Integrate Intial State with Curl Commands		|4			|   2			|

Arduino comes with an MQTT library implementation that was used. Simple code that translates sensor data into human readable test was added and the values were transmitted via MQTT to a predefined broker.

The hardware consists of an Arduino UNO, Ethernet Shield, LM35 and a Flow Sensor. The data is then received by a Node-RED application that converts the strings into numbers and display it on gauges and graphs. A screenshot of the dashboard is shown below.

![dash- Diagram](/assets/images/iot2020/dashboard1.png){: .align-center}

This is a local dashboard which is created using the flow diagrams in Node-RED. The figure below shows the flow diagram for my implementation.

![Flow- Diagram](/assets/images/iot2020/flow1.png){: .align-center}

The curl commands at the output nodes are used to parse the data from the system into REST requests which enables the Initial State Dashboard.

### Sub-Project 3 - LCD with Arduino IDE

This sub-module helps explain the ability of the IoT2020 to be used with the Arduino IDE. I was able to import the LCD driver library from SeeedStudios and use the LCD in this project. It is the simplest part of the entire design and does not need a development cycle. It serves as a case study that any existing Arduino code may be used with minor or no changes as long as the Arduino IDE is used. The user sketch run as a separate process and starts automatically after system boot.

## Video Demonstration

Here is a demo video of the final project with a bit of explanation of the design.

<iframe width="560" height="315" src="https://www.youtube.com/embed/GwnwsmUeEn0" frameborder="0" allowfullscreen></iframe>

## Code and Design Files

All the code and design files are available for download from [the GitHub project repository](https://github.com/inderpreet/iot2020_boilercontroller). I have made sure that the code contains sufficient comments to be reused by anyone and the entire project is distributed under the GPLv2 open source license.

## Lessons Learned

This project is a very essential demonstration of the capabilities of the IoT2020 as a maker platform and its flexibility in terms of coding languages and ease of use. The project was given the second prize in the competition at Hackster and I hope that other can use the information and instructions I have provided. 

Special thanks to RS Components and The Breadboard(Peter Oakes) for sponsoring the competition as well as support along the way.

