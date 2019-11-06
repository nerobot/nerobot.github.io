---
layout: post
title:  "Canbus Boiler Switch"
date:   
categories: canbus homeautomation
---

Now that winter is here, I have decided to finish the first draft of my canbus based boiler switch.

I did have a boiler switch connected to my home automation system (I'm using home-assistant as my main home automation system, which I will write about at a later date), but that was a two switch system and it used modbus instead of canbus. It was a two switch system because my old heater was a system boiler, so I had one relay for the heating and one for the hot water. I have recently updated to a modern combi-boiler, so I now only need a relay to control the heating. I was using modbus because it was easy enough for me to creat a library myself. However, the more I looked into it, the more I started to worry about some limitations of modbus, the main issue being the single master system allowing one slave to clog up the whole bus while it is waiting to reply.

Instead, canbus is a mulit-master sysem, allowing each node to send data as soon as it needs to, without having to wait for the master to request it (assuming the bus isn't busy). There are a number of reasons that this is better for my current system, but the main one is that it allows senor data to be sent from a node to my HA system almost instantatiously. Since I intend to have over 100 sensors in and around my house, this should help reduce some latency in the system. For example, when a doorbell is pressed, I don't want to wait until it is polled before HA is awear that the bell has been pressed.

# Canbus network

For my canbus driver, I'm using the mcp2551 transiever and the mcp2515 controller.

Using the mcp2515 canbus controller, I don't have to worry about actually implementing my own canbus driver. Instead, the mcp2515 will perform all of the timing, priority, and other canbus specification details. It is SPI controlled, so it's pretty easy to create a driver to send and receive messages over the bus.




