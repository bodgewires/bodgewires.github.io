---
title:  "Getting Started with TI RTOS and the Texas Instruments CC1310 Launchpad"
excerpt: "A quick look at how to make a TI RTOS Project using Code Composer Studio and a touch on POSIX"
header:
  image: /assets/images/unsplash-image-2.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - tutorial
tags:
  - TI
  - RTOS
  - CC1310
---

## Getting started with TI RTOS and CC1310

The CC1310 is a sub Ghz single chip solution that run its RF core on a Arm Cortex M0 and the Application processor is an Arm cortex M3 which means it is very flexible in terms of applications. Since things can get very complicated very quickly, TI recommends not developing native applications like for the MSP430 and AVR that is the bread and butter of most firmware. Instead, they recommend using TI RTOS to host your applications and provide a generous load of examples and what not to aid getting of the ground quickly. 

{% include base_path %}

{% include toc title="Contents" %}

Unfortunately, there is more than one way to skin a cat and Code Composer Studio can seem downright scary to the new-comer. In this article, I discuss the use of TI RTOS with CCS 7 and touch on pThreads for the POSIX aware readers out there.

## What is an RTOS

Here we go again! So from the wikipedia out there...

A real-time operating system (RTOS) is an operating system (OS) intended to serve real-time applications that process data as it comes in, typically without buffering delays. Processing time requirements (including any OS delay) are measured in tenths of seconds or shorter increments of time. They either are event driven or time sharing. Event driven systems switch between tasks based on their priorities while time sharing systems switch the task based on clock interrupts.

Having said that, my version is simply this. An RTOS is a software layer that allows you to write something simple like a function to blink and LED or read a button press and then ask the RTOS to manage things when you want other functions to work in addition to you blinky. These other functions can be listening to the radio or send rf data etc. Why RTOSs are a good ideas is because they allow you to not micromanage everything your processor or peripherals are doing and concentrate on one thing at a time. 

The official TI webpage can be found at http://www.ti.com/tool/ti-rtos

## The CC1310 sub GHz launchpad

This launchpad is very special since they are designed for low power and long range. When I say long range, I mean, 20KMs on a coin cell. Yea. Thats right! 

![alt text](/assets/images/tirtos/1.gif){: .align-right}

[Check this out](http://www.cnx-software.com/2015/12/18/ti-simplelink-cc1310-wireless-mcu-promises-20-km-range-20-year-battery-life-on-a-coin-cell/)

[and this](http://links.mkt102.com/servlet/MailView?ms=NTAyNzcwMDES1&r=MTE1NzI3Mzc1MjM3S0&j=ODIyNjg5MDY2S0&mt=1&rt=0)

So this means even without the whip antenna I can still get a decent range out of these modules and that's the reason I plan to use them in my ongoing project.

The official TI link is [http://www.ti.com/tool/launchxl-cc1310](http://www.ti.com/tool/launchxl-cc1310)

## Getting back to TI RTOS

We need a few tools to get started.

1. Code Composer Studio 7.x or above. [From Here](http://processors.wiki.ti.com/index.php/Download_CCS)
2. Smart RF Studio [From Here](http://www.ti.com/tool/smartrftm-studio)

Install em and create a workspace in your favourite location. There are now two ways to create a project. The first is to simple right click in the project explorer and select 'New CCS Project'

Flow the rabbit and select TI-RTOS empty (minimal) Example and give it a name.

<figure class="half">
    <img src="/assets/images/tirtos/2a.png">
    <img src="/assets/images/tirtos/2b.png">
    <figcaption>Click Click Click</figcaption>
</figure>

Press that hammer button to check if it compiles. It should. The example comes with a Blinking LED Task that allows you to check if everything is all right and if you connect and program your launchpad, you should be able to see things work. For a demo and instructions on method two, take a look at the video below.


<iframe width="560" height="315" src="https://www.youtube.com/embed/hsEFg2-tShM" frameborder="0" allowfullscreen></iframe>


## What is POSIX

Again a bit of Wikipedia here.

The Portable Operating System Interface (POSIX)[1] is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems. POSIX defines the application programming interface (API), along with command line shells and utility interfaces, for software compatibility with variants of Unix and other operating systems.

And the TI Wiki says...

SYS/BIOS (v6.42.01 and higher) provides a subset of the POSIX thread (pthread) APIs. These include pthread threads, mutexes, read-write locks, barriers, and condition variables. The pthread APIs can simplify porting applications from a POSIX environment to SYS/BIOS, as well as allowing the same code to be compiled to run in a POSIX environment and with SYS/BIOS. As the pthread APIs are built on top of the SYS/BIOS Task and Semaphore modules, some of the APIs can be called from SYS/BIOS Tasks.

[Link to original](http://processors.wiki.ti.com/index.php/SYS/BIOS_POSIX_Thread_(pthread)_Support)

In short, the pThread support is implemented on-top of the tasks modules so unless you want to port some POSIX code from another OS, just stick to the tasks system.

## What next?

A UPS notification puts some parts from Element14/Texas Instruments on my table next week. Until then I will be playing with the CC1310 a bit more and hopefully have something with RF Studio Next.

Thanks for reading and happy hacking,

