---
title: How to power your SBC
description: 
published: false
date: 2025-11-24T08:13:30.345Z
tags: 
editor: markdown
dateCreated: 2025-11-24T08:13:30.345Z
---

# 1. Introduction

Powering a Single Board Computer (SBC) reliably is a fundamental step toward building stable and efficient embedded systems. Yet, newcomers are often surprised by how many factors influence something as simple as “providing power.” This article outlines the essential concepts behind choosing the right power source, clarifies the often-misunderstood distinction between dedicated power supplies and battery-oriented chargers, and explores how cable design and USB/USB-C standards affect voltage stability and current delivery. By understanding these foundational elements, users can avoid common pitfalls, ensure consistent performance, and prolong the lifespan of their SBC hardware.

# 2. When do i have to consider this?
Whenever you have problems with random reboots, kernel panics, and/or non-working peripherals (especially power hungry devices like spinning hard drives), the first thing you should do is check your power situation. The operating system we deliver is rock-solid if your board has sufficient and reliable power.

# 3. PSU or Charger? Whats the difference?

The difference between these power bricks lies in their intended usage. A charger is designed to charge a battery, so it does not need to handle brown-outs. Brown-outs occur when the AC voltage of your home drops, which can happen due to various reasons. For example, a refrigerator requires a significant amount of power to start its compressor. When the compressor activates, it may draw so much power from your wall socket that the voltage in your entire home momentarily drops below the standard rated voltage for your country. This situation can cause a charger to temporarily stop supplying power. However, this is not an issue when using the charger to charge a battery-powered device because the device has its own battery to run on. A Single Board Computer (SBC), on the other hand, relies entirely on that power and may crash during a brown-out. 

- This is the voltage of a fridge. You can tell when it did turn on by looking at the voltage drop:
![voltage.png](/psu-charger/voltage.png)

A PSU (Power Supply Unit) is built to manage such situations. It incorporates capacitors that function like small batteries to compensate for brief drops in voltage, providing a stable power source for your SBC. 

## 3.1 How do i find out what kind of power brick i have?

Unfortunately, there isn't a reliable way to determine which type of power brick you have. However, you can make some assumptions to identify it. Generally, since a PSU requires more components, they tend to be heavier and more expensive. This doesn’t mean that an expensive power brick is necessarily a PSU, but you can assume that a cheap or free power brick (such as one that came with your phone) is likely a charger. 

For now, we recommend using the Orange Pi PD100W, which is a 100W USB-C PD-compliant power supply. It did suppries us in how well it is built and handles power delivery. 

Another great option is to purchase a Lenovo USB-C 65W laptop power supply. These can often be found at reasonable prices in the used market and work very well with our supported SBCs. 

