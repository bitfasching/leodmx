# LeoDMX

A software DMX-512 implementation for Arduino Leonardo & Micro:
- uses HardwareSerial for clean UART data transfer
  (writes to digital pin 1 and uses Serial1 per default)
- sets a driver enable flag to HIGH during transmit
  (uses digital pin 2 per default, can be disabled entirely)
- clean, lightweight and simple: send a DMX frame with a single function call
- synchronous operation only, which means:  
  - doesn't clash with your timers!  
  - predictable access of resources and pins!  
  - you can't do other stuff in the meantime  


## Why do I need this?

[DMX](https://en.wikipedia.org/wiki/DMX512) is a standard for controlling peripherals over a two-wire bus which is commonly used for stage lighting. If you have any RGB LED stage spots, chances are they have a XLR connector and can be controlled via DMX. Since DMX is a bus system, daisy-chaining allows for connecting a lot of devices.


## DMX hardware

This library allows to produce a DMX-like digital signal, but it's only single-ended (alternating between your supply voltage and ground). In order to be compatible with DMX (and being able to reliably send data through a longer cable in general), you need a symmetric signal according to [RS-485](https://en.wikipedia.org/wiki/RS-485). To do so, use a RS-485 transceiver IC. Connect the data input to pin 1, and optionally the driver enable input to pin 2 for saving power when no data is sent. Using a slew-rate limited chip such as the [MAX483](https://datasheets.maximintegrated.com/en/ds/MAX1487-MAX491.pdf) makes your setup more tolerant to bad cables and minimizes the risk of interference in its surroundings.


## Getting started with examples

Drive a complete DMX universe with an Arduino! Either write your own sketch using the library or flash one of the examples. If you connect the Arduino to a computer via USB, you may use the included Python scripts to pass your channel data to the Arduino. Note that some parts were created for specific use cases on a Linux machine, please review and change according to your setup. Depending on your system's settings for accessing serial devices, you may try to run the scripts as root.


## Reference

It's really easy, see the public methods in [LeoDMX.class.h](LeoDMX.class.h) and the example [serial2dmx.ino](examples/serial2dmx/serial2dmx.ino).
