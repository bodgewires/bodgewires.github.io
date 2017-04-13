---
title: "Project-While You Were Out"
excerpt: "Using the Cypress Analog CoProcessor and a Raspberry Pi 2, we automate and Office"
header:
  image: /assets/images/whileuwereout/splash.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories: 
  - Project
tags:
  - PSOC
  - Linux
  - OpenHAB
---

## The Problem Statement

Like many people, I work in a room with a workbench, lights, fans, Air-Conditioning and bench test equipment etc. During work hours I have a habit of taking trips away from the bench for a multitude of reasons which includes

{% include base_path %}

{% include toc title="Contents" %}

* visits to the little boy’s room,
* taking personal phones calls,
* 15 minutes fresh air breaks after an hour or an hour anda half and even
* little snack breaks.

These away from bench breaks vary in time and have no fixed schedule(well at least not one that I have established) and during this time, every electrical equipment consumes power. The short wastage durations can accumulate to large annual ones and this is the basis for my problem statement. We want to accomplish the following tasks:

* Detect user presence
* Control Various appliances in the office which includes Lights, Fans and Airconditioning/HVAC
* Provide Intelligence management in user absence.
* Provide Remote Control and Monitoring.
* Add a Security System to the Office

## The Solution- "While you were away"

The proposed solution is titled “While You Were Away” because we intend to “sense” when the user is away and optimise consumption in his/her absence. The solution is much more than the simple Motion detector combo because the plan is to implement programmability to the automatic control aspect. The block diagram below shows the various hardware components and their interconnects in the final design.

![alt text](/assets/images/whileuwereout/2.jpg){: .align-center}

The system is composed of 4 major components. The heart of the system is the Cypress PSOC Analog Coprocessor kit which interfaces with five sensors. A Raspberry Pi 2 is used to run OpenHAB Software that provides the GUI as well as other features. An MFRC522 board is used to scan RFID tags and a relay board is used to interface with electrical appliances. The PSOC runs a custom hardware/software design that is provided on github for download. The Analog Coprocessor reads sensors and stores the values in its internal memory. The raspberry pi 2 communicates with the PSOC kits over I2C and retrieves this data. A python script is used to parse the sensor values and then passes them on to an MQTT broker at iot.ecliplse.org . This architecture is chosen to facilitate future customisation where the PSOC may talk to an MSP430(Code provided) and send the data either via USART or other means.

The python script also enables reading of the RFID tag and listens to specific MQTT topics for commands. These commands are used to toggle the relays which in turn controls appliances. The rules engine, GUI and data logging is provided by OpenHAB which is a free home automation software solution. It runs on the Raspberry Pi 2 as well but can be a remote installation as well for IoT like applications.

## Video
Here is a short demo video of the project. Be sure to Check it out

<iframe width="560" height="315" src="https://www.youtube.com/embed/r_VpPWnMmHs" frameborder="0" allowfullscreen></iframe>

For anyone who wants to duplicate this projects, here is an overview of the steps involved. All software components are provided for free download as well.

## Here is what I did.

The first step is to download the code from https://github.com/inderpreet/Project-WhileYouWereOut

Install PSOC Creator from http://www.cypress.com/products/psoc-creator-integrated-design-environment-ide and compile and program my PSOC design to the kit.

See this video for details.

<iframe width="560" height="315" src="https://www.youtube.com/embed/awuQyhztke0" frameborder="0" allowfullscreen></iframe>

After this, the Coprocessor kit should be ready. Next we need a Raspberry Pi (2) where we download the rest of the files. Follow the instruction at

https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c
https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-spi

For setting up the Raspberry Pi’s GPIOs

Hookup the PSOC’s I2C lines and the MFRC’s SPI lines as given here( https://github.com/mxgxw/MFRC522-python )

One more thing! We need a logout button so solder up wires to your push button and connect it to the last two GPIOs

Install the dependencies using

```bash
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install 
sudo apt-get install python-smbus 
```

Next run the setup script from the SPI folder using sudo python setup.py install

Finally, run the software using

```bash
sudo python coprocessor.py 
```

If everything is done right it should start the service. If you get I2C errors, check the connections for loose wires. They are the most common culprit.

Next, Install and setup openHAB as per instructions

http://docs.openhab.org/installation/

Copy the Sitemap, Items file and rules file that you downloaded.

Phew! that a lot of work but its worth it.

Finally start OpenHAB and it should work.

Download the STL files from https://pinshape.com/items/32437-3d-printed-psoc-while-you-were-out and 3D Print them

![alt text](/assets/images/whileuwereout/1.jpeg){: .align-center}

Put everything together and viola!

## Closing remarks

This project is a demonstration of how the Raspberry Pi can be interfaced with other hardware and analog sensors to create something more. The Cypress Analog Coprocessor takes care of the sensor interfacing part and the user is able to focus on the other components. I have provided all the STL files as well as the code for download at github as well as code for the Arduino/Energia to be used for testing and interfacing the PSOC Design. I hope this project can serve as a useful reference for other experimenting with the board.

Thanks for reading.