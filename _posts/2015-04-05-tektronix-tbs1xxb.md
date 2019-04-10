---
title:  "Review - Tektronix TBS1xxb oscilloscope"
excerpt: “An Oscilloscope review and some usage information on scopes in general"
header:
  image: /assets/images/unsplash-image-2.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Review
tags:
  - instrument
  - bench
  - tools
toc: true
toc_label: "Table Of Contents"
toc_icon: "book-open"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## INTRODUCTION

The Tektronix – TBS1XXXB-EDU series of Oscilloscope have been targeted towards the educational sector. The logo on the front panel that says “Enabling teaching” is proof of that. The traditional approach has been to carry a paper manual where the students will find the detailed instructions to the experiment to be performed. The experiment is setup on a breadboard or on a kit or sorts.
The EDU series allows for the instruction manual to be integrated onto the oscilloscope itself. The details are
‘assembled’ in the courseware software and then put onto the scope.

This review is for the TBS1202B-EDU which is the top of the line model in the series.


## Specifications and Key features

* 200MHz BW
* 2-channel model
* Up to 2 GS/s sample rate on all channels
* 2.5k point record length on all channels

## KEY FEATURES

* 7 inch WVGA (800X480) Active TFT Color Display
* 34 automated measurements
* Dual window FFT, simultaneously monitors both the time and frequency domains
* Integrated Courseware feature
* Dual channel frequency counter
* Zoom Function
* Autoset and signal auto-ranging
* New affordable 50 MHz TPP0051 passive probes
* Multiple-language user interface
* Small footprint and lightweight – Only 4.9 in. (124 mm) deep and 4.4 lb. (2 kg)
* 5Yrs warranty

## Package Contents

The package contents were pretty straightforward. Along with the unit was a power cable, manual, CD, Calibration certificate and two probes model TPP0201.

![alt text](/assets/images/tbs1xxb/oob.jpg "Out of the Box"){: .align-center}

Out of The Box

I was initially a bit disappointing with the probes which are a fixed 10x attenuation probes and felt a bit ‘cheap’. But I am comparing with the probes I used with the MSO2024B.

![alt text](/assets/images/tbs1xxb/probes.jpg "TPP0201 Probes"){: .align-center}

TPP0201 Probes

Considering the price I think they are worth every penny.

## Pricing

The website quotes a price of Rs. 39,000 for the base model. I am not sure what would be the pricing in your country but I have always found the Tek scopes worth the money. This scope is no exception. The element14 website quotes it at 127,575.00INR which is quite decent for a 200MHz scope with the kind of functionality it provides.

## First Impressions

I have used Tek in the past and I will try not to compare with the MSO2024B which is a mixed signal scope with 4 analog channels. My first impressions when I first set it up were…

* Very nice display. Its big and the resolution is 800×480 which makes the whole unit more usable No more squinting to look at the display.
* Portable. The scope is lighter than others which is a good thing. Build quality is good with no ‘squeaky’ joints.
* Only two channels: I would have liked to see 4 channels but I guess it is OK for this segment.
* No Function Generator: Since this scope is marketed as an educational scope, it would have been value addition for it to have a function generator integrated into the unit. I was able to rig up one using an AD9850 and a microcontroller so I guess it would not have cost the designers an arm and a leg.
* No clicky knob: Now this may sound a biit strange but bear with me. The knobs are rotary encoders which give a ‘clicky’ feel when turned. I miss that in the main dial and since it drives a menu interface which has the selection ‘clicking’ to an item, it made sense. The knob is smooth to turn but they could have used the same type used in the voltage gain selection knob.
* No VGA/ HDMI out: In teaching to a lab full of students, it is beneficial to have the output stream to the projector. Since the courseware software allows for the instructions to be put onto the device, the additional VGA port would have made it much more useful.
* No bus decoding options: There is no support to upgrade this model with the decoder modules. I know they are industry requirements, but this instrument can bridge that gap.

There was a sticker on the display that notifies you to update the firmware and also to register with Tek. I thought that was a nice addition.

## Project 1: Getting started with a sine wave

As mentioned before, I would have liked to see a function generator but since it was not there, I decided to make my own. Using an arduino and an AD9850 module, I put together a little test piece in a hurry. I will be sharing the entire details and linking them here. The code will be available at github.com/inderpreet

<iframe width="560" height="315" src="https://www.youtube.com/embed/AWv1dOTgSCY" frameborder="0" allowfullscreen></iframe>
<br />
<iframe width="560" height="315" src="https://www.youtube.com/embed/AWv1dOTgSCY" frameborder="0" allowfullscreen></iframe>


## Project 2: Basic Rectifier

It is always interesting to see the effect of load on any filter. Hence my next demo is a simple rectifier with a filter cap. When the load is varied, the o/p varies demonstrating the charging and discharging of the filter CAP.

[Pics Missing]

The FFT shows how the frequency components vary.

## Project 3: Filter implementation using Microcontroller

It is possible to do do small frequency filtering with a microcontroller like MSP430. This segment is under construction and I will be updating it very soon.

## Project 4: Batman Logo on the scope

There are a lot of people who have given various methods to achieve this but I am interested in doing this using MATLAB or MATHEMATICA. Again right now it is under development and will be updated soon.

## Feedback

I tried to use the scope for teaching 1st year engineering students and here are my impressions:

* As a teaching aid, a few things like VGA out would have been nice. But beyond that, I was quickly able to deliver sessions without a hitch. The menus system is clear and ergonomically designed the scope allows even a newcomer to get comfortable easily. The presence of a function generator would have reduced the number of instruments on the bench.
* The courseware software was easy to use but the traditional paper handout approach is a bit better. I found the students struggling to move around the scope.
* The main menu dial feels a bit delicate for the use of students. Students tend to be a bit harsh with their usage but the scope overall feels solidly built. Another thing was the probe connector- I might end up doing a teardown to see how the connector binds to the inside. The New MDO series has the connectors screwed to the PCB and not just soldered to it.

## Dual window feature

The dual window feature allows for the time and frequency domain waveforms to be viewed simultaneously. This sounded much nicer than it actually was. The signal waveforms are relatively on a small portion of the screen so it was a bit disappointing.

<iframe width="560" height="315" src="https://www.youtube.com/embed/AWv1dOTgSCY" frameborder="0" allowfullscreen></iframe>


## Automated measurements

This sounds very boring but it is actually one of the most useful features. The scope presents multiple measured values which is a big help when explaining the properties of a signal. There is a long list of possible measurements that can be done. As a test equipment, this scope rocks!

<iframe width="560" height="315" src="https://www.youtube.com/embed/11sAHCW00YA" frameborder="0" allowfullscreen></iframe>

## Waveform inspector

The waveform inspector is a feature that is present in the more advanced products which allows for the use to scan the captured waveform for events like rising and falling edges. This is extremely useful when working with digital signals. The 2.5K sample memory is not the largest and I have logic analyzers with more depth but it is still a useful feature none the less.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SKRdTD_k2Hg" frameborder="0" allowfullscreen></iframe>

## Summary

Even though Tek put a lot of thought on how to make this an educational scope, I think a few points were missed.
On the positive front,

* Good build quality
* big display
* automated measurements
* low cost

are the highlights of this scope.

On the negative front,

* lack of VGA port
* only 2 channels

are the lows.

The courseware system will work for a lot of people and labs but for the Indian scene where it is more convenient to use the handout approach, its not a selling point. A small bandwidth function generator would have been a nice addition to the instrument since most lab experiment will almost always require one. All in all a great piece of test gear from Tek which can not only be used for education but for commercial use as well.