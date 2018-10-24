---
title:  "Intel Edison Based Garden Management System"
excerpt: “Using the Intel Edison, we automate the garden, soil and hydroponic."
header:
  image: /assets/images/edisongardner/splash.jpg
categories:
  - Project
tags:
  - Linux
  - OpenHAB
  - Edison
---

## INTRODUCTION

A lot of people think about starting gardening as a hobby and some even imagine growing their own vegetables and fruits at home. However as a consequence of busy schedules, most of us will never get the time to maintain the garden the way we want. Plants need consistent care and look after to flourish and bear fruit and with the advent of technology, we may be able to setup an electronic system to take over the chore of garden maintenance. This is the premise of our project, Edison The Gardener.



There are two common types of growing solutions that are common these days.

* One is the standard growing in the soil gardening where we use soil mixed with organic fertiliser to grow plants. Plants are planted in the soil and we only need to add water and light. In our setup, we use large pots to grow plants in direct sunlight and watering as well as soil measurement is done via the Intel Edison.

* The second is called a hydroponic system where instead of soil we use a different medium to grow plants and the nutrients are supplied as a part of the liquid system. In our setup, we use perlite as a growing medium and use liquid nutrients pumped in a Flood and drain system. The nutrient liquid is pumped into the tray and kept there for a time and then drain afterwards and cycled.
Our project is designed to cater to both these needs and can be extended as per requirement.
Here is a demo video of the final system:

<iframe width="560" height="315" src="https://www.youtube.com/embed/WRDkfvEQK3E" frameborder="0" allowfullscreen></iframe>


## DESIRED FEATURES

For this system the following features were consider desirable and were user as a system specification to design around.

1. A SMART garden watering solution for the traditional garden which is able to track the irrigation cycles and the moisture levels of the system. Since we are talking about IoT we should be able to take advantage of the facilities of the internet namely the Weather Service. The system should be SMART enough to not water the plants if the soil is already wet OR if rain is predicted in the near future.

2. A solution for indoor gardening with lighting and temperature control and monitoring. We want the ability to grow off season crops that we can plant in a small greenhouse or our own kitchen and for that we need to control additional elements of lighting and temperature inside.

3. A hydroponics system which can be monitored and controlled via a GUI. Instead of a traditional hydroponics timer, we use the advanced capabilities of the system to remotely measure and control the operation of a hydroponics system. We want the ability to set complicated rules for the control of our hydroponic growing system

4. A data logging facility to track various parameters. We need to be able to log the system data for analysis by expert should our garden begins to fail.

5. A visual data display for all measured quantities. We understand that data visualisation can help understand monitored data better hence we want the capability to see the data in a graphical way over the internet.

6. A configurable alert system for events. We want the capability to set alerts for certain events such that corrective action can be taken. If possible we would like the ability to get alerts on our Android devices.
Wow! Thats a lot of desired features but thanks to the incredible power of the Intel Edison and simplicity of Node.js and openHAB, we were able to get all that done… and more.

## DESIGNING THE SYSTEM

The hero of our system is the Intel Edison with the SeeedStudios sensors kit. A basic block diagram of the system is given below which shows the various elements of the project.

![alt text](/assets/images/edisongardner/1.png){: .align-center}

The diagram shows there are two sub setups which are explained as follows:

### The outdoor setup.

The outdoor setup consists of a soil based configuration for growing plants. We have chosen large pots with soil and fertiliser and these are placed outside in the sun. A water reservoir has a pump that can be switch on and off using the intel Edison and we also have a moisture sensor to detect the condition of the soil.

### The Indoor setup.

The indoor setup consists of a hydroponic setup with a nutrient solution tank, a flooding pump to fill the hydroponic tray, a drain pump to empty it. We also have a artificial lighting lamp with a UV light as well for indoor lighting and sensors to detect the correct operation with a light and temperature sensor. The Flood tray also as water sensors to detect incomplete filling of the tray indicating insufficient water or a defective water pump.

In addition to these, we have the Intel Edison with the SeeedStudios grove sensors which is connected to a local Intel Galileo. This Galileo hosts an existing home automation setup using OpenHAB. It is also connected to the internet via the local network and Wifi and talks directly to the Intel Analytics Cloud to log and graph data.

The software architecture is explained in the diagram given below.

![alt text](/assets/images/edisongardner/2.png){: .align-center}

The Intel Edison runs a Node.js script that initialises the peripherals, drives the sensors and actuators, converts the data into human readable form and exposes an API to remotely control everything. Essentially, the Node.js script subscribes to an MQTT broker on a particular topic and waits for commands. There are some low level tasks taken care of as well such as making sure nothing overflows etc but the API is used to get and put data from the Intel Edison. In addition to this, there are dedicated sub tasks to post sensor data periodically to the Intel IoT Analytics Cloud. Hence the cloud analytics section can function independently of any control.

The sensor data is also retrieved by OpenHAB which has a set of rules that are used to control the system. The logic part as well as the GUI is created using OpenHAB running on the Intel Galileo. A local version of the data is also captured in a MongoDB for creating graphs etc.

The GUI generated by OpenHAB is shown in the image below.

The library support by Seeed and Intel for the sensors and actuators is phenomenal and are available here:
https://software.intel.com/en-us/iot/hardware/sensors

The two setups Outdoor and Indoor are made separately and are explained in steps a-b and c-d respectively. The setup of the Intel Edison is explained in steps e-f so if you would like to skip to a particular section, feel free.

## SETTING UP A DIY SOIL GARDEN

The first step is to create a small soil garden and in our setup, we used a variety of pot which ranged from large enough for growing vegetables and smaller ones for herbs.

The next step is to put together some soil which is free from rocks etc and which has been heat treated to get rid of any pests etc. In our setup we added 50% soil with 50% organic manure locally available and mixed it together. The pots were drilled small holes at the bottom for the water to flow out and we placed jagged rocks around the holes so that they do not get blocked by flowing dirt. The soil was then potted as a dry mixture and all the pots were set aside.

Next we purchased some quality seeds for chillies and eggplants and germinated seedlings for tomatoes. The seeds were planted 1-2cm deep while the tomato seedlings were planted deep enough to cover the entire root system. These are cover with the soil and patted down a bit and then watered heavily because the soil will need a lot of water the first time.

<figure class="half">
    <img src="/assets/images/edisongardner/3.jpg">
    <img src="/assets/images/edisongardner/4.jpg">
    <figcaption>Fresh soil</figcaption>
</figure>

We also recycled an old cabinet drawer as a herb garden where we laid out a sheet of plastic across the entire inside of the wooden construct.

Next we drilled out a hole for a place where the water should drain and then added a piece of pipe to it though the plastic sheet. We then used a sealant to make the whole connection water-proof. Next we laid out the bottom with small rocks to form a layer where the excess water can drain through. The drawer is placed such that there is a slant towards the drain hole.

<figure class="third">
	<img src="/assets/images/edisongardner/5.jpg">
	<img src="/assets/images/edisongardner/6.jpg">
	<img src="/assets/images/edisongardner/7.jpg">
	<figcaption>Water Drain</figcaption>
</figure>

Next we positioned the pots and the herb garden next to a windows through which the pipe and cables for the sensors will come through. This is done because in our setup we also have an indoor setup which is controlled by the same Intel Edison. An irrigation pipe is brought through the entire setup and circulated. Small holes are cut in the rubber tubing such that water can flow out and into the pots etc. The pump is chosen such that it has the capability to generate the necessary pressure.

![alt text](/assets/images/edisongardner/8.jpg){: .align-center}

You can choose to decorate and make things pretty as per your convenience. In our setup, we used paint to make the pots and bricks the same color as well as the garden area was covered with small pebbles to improve the aesthetics. With this, the outdoor setup is complete and all we need to do is connect the pump as well as the sensor to the Intel Edison. That is explained in later steps.

![alt text](/assets/images/edisongardner/9.jpg){: .align-center}

## SETTING UP A DIY HYDROPONICS GARDEN

A hydroponics system is a soil-less growing system where the potting media used does not retail water like normal soil. There are many subtypes and these can be understood by visiting [LINK TO Hydroponics] The one we used is the Ebb n flow hydroponics where the plants are placed in a tray and the water with the nutrient mixture is pumped to flood the tray for some time. Then this tray is drained and the mixture is returned to the reservoir. This saves water as well avoids the drawbacks of the typical soil garden.

In our setup, we used perlite as a medium which was purchased off ebay. This perlite is washed with water and chlorine and the granules are dried.

We used plastic cups and cut multiple slots(Smaller than the perlite granules to allow outflow and inflow of water. You may also use netted materials as well to retain the perlite if the small slots do not work right for you. Two such glasses were sandwiched together to form a barrier to retain the perlite. Pebbles were placed at the bottom to allow the containers to be weighed down and not float up as the nutrient solution is pumped.

![alt text](/assets/images/edisongardner/10.jpg){: .align-center}

These are then filled with perlite and a group of six such vessels were arranged in a plastic tub. We fitted the tub with water tight glands to allow connecting the water pipes. You can choose to use smaller or larger glands to suite your needs.

![alt text](/assets/images/edisongardner/11.jpg){: .align-center}

We use a plastic tray to act as the flood tray and we fitted it with a gland for the drain connection at the bottom and one gland near the top to act like an overflow should the sensor ever fail. Scotch tape was used to hold the planers in place because the flooding water will make them float up. Water should slowly creep up into the perlite as well as drain out easily.

<figure class="half">
    <img src="/assets/images/edisongardner/12.jpg">
    <img src="/assets/images/edisongardner/13.jpg">
    <figcaption>Hydroponics Container</figcaption>
</figure>

We were able to fit six planters in one tray. Two buckets are used as reservoirs to hold the water for the Soil Irrigation system as well as the nutrient mix for the Hydroponics system. Two submerged pumps are deployed as shown.

![alt text](/assets/images/edisongardner/14.jpg){: .align-center}

For the Lighting system we used a table lamp with a CFL lamp and added a UV lamp to it. For our experiment, we salvaged a UV Lamp from an old water purifier.

<figure class="half">
    <img src="/assets/images/edisongardner/15.jpg">
    <img src="/assets/images/edisongardner/16.jpg">
    <figcaption>Salvaging a UV Lamp</figcaption>
</figure>

All these elements are setup on a table inside our room which will act like a greenhouse. We used a SeeedStudios Pump to drain the hydroponics system and its simply setup to pump the water back into the reservoir. For decor we employed some hand made chart and cardboard box backs. Paint and coloured tape was used to make things beautiful.

This readies our Hydroponics hardware.

## Setting up the Sensors and connecting the motors and Lamp

The Sensors are all connected via the SeeedStudios Grove System. The parts include:
1. Seeed Moisture Sensors
2. Seeed Water Level Sensor
3. Seeed Water Pump
4. Seeed Relays
5. Seeed Light Sensor
6. LM35 as a temperature Sensor
7. Seeed Gas Sensor

We used a grove base shield to connect all the parts and to mount the sensors, we designed and 3D Printed a simple stand.

<figure class="half">
    <img src="/assets/images/edisongardner/17.jpg">
    <img src="/assets/images/edisongardner/18.jpg">
    <figcaption>Sensors</figcaption>
</figure>

We needed more relays hence made a few expansions ourselves. WARNING: Working with mains is dangerous. Adult supervision is a must for kids. A single PCB with a BC547 to drive the relays was made and enclosed in a small plastic casing.

<figure class="half">
    <img src="/assets/images/edisongardner/19.jpg">
    <img src="/assets/images/edisongardner/20.jpg">
    <figcaption>Relay Casing</figcaption>
</figure>

In order to connect the Lamp and the Pumps, the following diagram was created and followed:

[Image for Electrical Connects]

The sensor wire for the moisture sensor had to be very long and was created using wire from the local hardware store. We soldered the ends so that there were connectors at both ends.

![alt text](/assets/images/edisongardner/21.jpg){: .align-center}

The level sensor for the Hydroponics tray was strapped in place using scotch tape and we made sure the sensor 
face did not touch the wall. If it does, it may retain moisture and give a false sensor output even when the tray is empty.

![alt text](/assets/images/edisongardner/22.jpg){: .align-center}

This readies the basic sensor setup.

## Creating an Enclosure for the Edison and 3D printing a mount for the sensors

We wanted to do something different for the enclosure and so a pyramidal design was chosen. We use a cardboard mockup to size up the required enclosure.

![alt text](/assets/images/edisongardner/23.jpg){: .align-center}

Once the size of the faces was verified, we then proceeded to cut acrylic sheets to form a pyramid shape for our enclosure. These sheets were glued together to form the final structure and a small stand was also constructed for the LCD. One side is left open for airflow for the sensors.

![alt text](/assets/images/edisongardner/24.jpg){: .align-center}

This finishes the hardware part of the build.

## Setting up the Edison, Intel IoT and Intel XDK

The Intel Edison can be programmed via a multitude of ways including Arduino IDE, Python and Node.js. Intel XDK for Node.js can be downloaded from Intel’s website and the links are given below.

- Setup guides for the Edison: https://software.intel.com/en-us/iot/library/edison-getting-started
- Setup guide for the Intel Iot Cloud: https://software.intel.com/en-us/intel-iot-platforms-getting-started-cloud-analytics
- Intel XDK Downloads: https://software.intel.com/en-us/iot/downloads
- Static IPs on Edison: https://communities.intel.com/thread/49348

The program is written to be a service that will send and receive data via MQTT to a local MQTT Broker service. The Edison periodically sends data to the Intel IoT Analytics service as well for logging.

![alt text](/assets/images/edisongardner/25.png){: .align-center}

## SETTING UP OPENHAB

A guide to setting up OpenHAB is given on my blog at:

https://embeddedcode.wordpress.com/2014/08/12/obligatory-install-tutorial-for-rpi-and-openhab/

These instructions may change with time hence are located externally.

Here is the link to the OpenHAB wiki where a lot of use cases have been already explained.
Configuring rules on OpenHAB is quite easy and works in a scripting language similar to javascript.
Our openhab configuration is attached at the end. Simple copy these files to their respective directories and you are good to go.

## MQTT brokers and setup a local connection

An MQTT broker runs on the Edison itself at port 1883 so no need to sweat. We just need to connect our openhab to it so we need it’s IP. Here is an example of a simple switch with MQTT.

## CONCLUDING REMARKS

This project is lot bigger than an instructable and we are making a dedicated page on my blog for it. The objective of this instructable is to give you pointers on where to start. Where you take it from there is upto you. This project and everything in it including the Hardware, software and presentation was done by me and my wife. If you like our project, give it a vote. Me and my wife worked pretty hard to put things together and we appreciate you taking the time out to go through this instructable. We hope it can be useful for you as well.

Thanks

## References and External Links

https://github.com/inderpreet/Edison-TheGardener