---
layout: post
title: "Harness the Power from the Mobile phone's Audio Jack (PCB practice)"
description: ""
category: 
tags: []
---
{% include JB/setup %}

Inspired by the [paper](https://web.eecs.umich.edu/~prabal/pubs/papers/kuo10hijack-islped.pdf) on "Hijacking Power and Bandwidth from the Mobile Phone’s Audio Interface". I decided to try it out and see if it is powerful enough to power my Leonardo Arduino.

##Schematics and PCB design

###Schematics 
Basically the circuit has its input from the left side connector and the input signal goes through a 1:20 micro-transformer to increase the voltage. Afterwards there is a rectifier circuit constituted by 2 N-mos and 2 P-mos which will flip the negative voltage to positive. The Schottky diode after the rectifier is just to prevent current from flowing back (due to the discharge of following capacities). In the end, filtering capacitors are placed to have a smoothed output voltage.

{% picture [preset] power_schematics.png alt="Schematics" %}
[Schematics in pdf](https://drive.google.com/file/d/0B1QY_8aEaeLeTlJYc2hvTVlPVUE/view?usp=sharing)


###PCB
{% picture [preset] pcb_front.png  %}
{% picture [preset] pcb_back.png  %}

Tips I got from experienced PCB designer:

- The thickness of traces: A good value is everything greater than or equal to 16mil (0.4mm)

- The spacing/isolation between the polygons (filling) and the wires: A good value is 20mil (0.5mm). The parameter usually is called "isolation", "spacing" or "clearance". Please do that with the fillings on both layers.

- Generate thermals for vias" or anything like that. When added thermals however, small "cutouts" are created around the hole which prevent the heat from "flowing away". 


##Solder the components on the PCB
I got the etched PCB from university's lab. I still need to place the components like mos-fet, diode and mini-transformers. Because these components are SMDs, Soldering paste has to be applied first on the pads before you actully place the components on it. After that, the PCB is sent to a reflow oven to be "cooked".



{% picture [preset] cooked_pcb.jpg  %}

The finished board is like this:

{% picture [preset] pcb_done.jpg  %}


To test the circuit, I installed signal generator App on my Android phone. Set the signal to maximum dB and at 20kHz.
In the picture below it shows the output signal on the ociliscope, with around 5.6V. (Here, an Led and a resistor is the load)
{% picture [preset] ociliscope_phone.jpg  %}

In the end, I didn't soilder the LED, because it is wasting the power. I only put one filtering capacitor of 10uF.
I try to use it to power my Arduino Leonardo, but it doesn't work. It seems that the board is trying to boot, but not enough power. However, because I don't have a low power ATmega or a Msp430, I couldn't test what is achieved in this [paper](https://web.eecs.umich.edu/~prabal/pubs/papers/kuo10hijack-islped.pdf).



