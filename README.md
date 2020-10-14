# Feather STM32WB55

## WARNING: Work In Progress

This is a work in progress, it may not work at all.  :)

## Overview

I have several (Adafruit Feather)[https://www.adafruit.com/category/943] boards, and Adafruit handily publish the (Feather Specification)[https://learn.adafruit.com/adafruit-feather/feather-specification] here to make your own.  

I recently discovered the STM32WB series of microcontrollers which include Bluetooth connectivity and decided to build my own development board around it.  This repository is my first attempt at designing it and builds upon the great work of several sources (see Acknowledgements below).

The ultimate goal is to get this board working and running [CircuitPython](https://circuitpython.org/), once working I may do another revision with a focus on enabling more of the low power features of the STM32WB series.

## Schematic

![Schematic](images/schematic.png)

## PCB

![PCB with inner layers](images/pcb1.png)

![PCB without inner layers](images/pcb2.png)

## 3D Render

![3D Front](images/3d-front.png)

![3D Back](images/3d-back.png)

## TODO

* Create footprints for the smaller WS2812B-mini 3.5x3.5mm Neopixel
* Create footprints for the [Fractus Antenna](https://fractusantennas.com/compact-reach-xtend-nn01-102/)
* Do I need a matching network?  STM sell a ready-made part [MLPF-WB55-01E3](https://www.st.com/en/emi-filtering-and-signal-conditioning/mlpf-wb55-01e3.html)

## Acknowledgements

* [Adafruit](https://www.adafruit.com/)
* [YouTube: Phil's Lab](https://www.youtube.com/c/PhilS94/videos)
