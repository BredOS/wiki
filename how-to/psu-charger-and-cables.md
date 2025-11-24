---
title: How to power your SBC
description: 
published: false
date: 2025-11-24T10:17:20.293Z
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

For now, we recommend using the [Orange Pi PD100W](http://www.orangepi.org/html/hardWare/powerSuppliesAndCables/details/PD100W-EU.html), which is a 100W USB-C PD-compliant power supply. It did suppries us in how well it is built and handles power delivery. 

Another great option is to purchase a [Lenovo USB-C 65W laptop power supply](https://www.lenovo.com/gb/en/p/accessories-and-software/chargers-and-batteries/chargers/4x20m26276). These can often be found at reasonable prices in the used market and work very well with our supported SBCs. 

A third option is the PSU of an Apple Macbook, as long as you choose the [USB-C version](https://www.apple.com/uk/shop/product/mxn53b/a/70W%20USB-C%20Power%20Adapter) of it.

## 3.2 How to determine the power output of my brick?

While most chargers and power supplies advertise their maximum power output, this is not true for all voltages they support. If we examine the Orange Pi PD100W, its specifications are listed on both their product page and on the power brick itself. To determine the power output in watts, you need to multiply voltage by amperes.

<br>

$Voltage * Ampere = Watt$
<div style="display:flex; align-items:flex-start; gap:20px;">

<div style="flex:1;">
  
<br>
  
| Voltage | Ampere | Watt |
| ------- | ------- | ------ |
| 5 Volt | 3 Ampere | 15 Watt |
| 9 Volt | 3 Ampere | 27 Watt |
| 12 Volt | 3 Ampere | 36 Watt |
| 15 Volt | 3 Ampere | 45 Watt |
| 20 Volt | 5 Ampere | 100 Watt |

From this list, we can determine that this brick is capable of powering an Orange Pi 6 Plus, as it requests 20V from the brick, providing up to 100W for use. Its predecessor, the Orange Pi 5 Plus, requests 5V from the brick and receives only 15W with this power supply. This amount is barely sufficient to power this SBC since its chip (RK3588) can draw 15W on its own. Additionally, the product page of the Orange Pi 5 Plus states its power requirement as 5V/4A or 20W.
  
</div>

<img src="/psu-charger/100wpsu.png" style="max-width:350px;">

</div>

## 3.3 What is USB-C Power Delivery and why does it matter?

As shown in the table above, chargers and PSUs that adhere to the USB-C PD standard can offer multiple output voltages. If your power brick, SBC, and cable (more on cables later) all support PD, your devices have the capability to communicate over the USB-C cable to determine acceptable voltages and amperes for both the power brick and the SBC. This communication allows them to select the best possible combination. Not all devices correctly support or implement this feature. For example, the Orange Pi 5 Plus does not support USB-C PD despite using a USB-C port to power the board. In contrast, the Radxa Rock 5/5B supports USB-C PD at 9V/2A, 12V/2A, 15V/2A, and 20V/2A.

As USB-C Power Delivery is part of the USB-C feature set it is not supported by USB-A. If USB-C PD communication does not happen your output voltage of your brick is 5 Volt.

> The USB-C PD communication should always occur at 5 Volt, but there are power bricks that have implemented this feature incorrectly. These power bricks might attempt PD communication at the last known voltage, potentially damaging your SBC. Such bricks are rare but do exist.
{.is-warning}

# 4. Cables; aren't they all the same?


