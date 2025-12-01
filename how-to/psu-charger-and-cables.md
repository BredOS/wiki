---
title: How to power your SBC
description: 
published: true
date: 2025-12-01T10:14:39.060Z
tags: 
editor: markdown
dateCreated: 2025-11-24T08:13:30.345Z
---

# 1. Introduction

Powering a Single Board Computer (SBC) reliably is a fundamental step toward building stable and efficient embedded systems. Yet, newcomers are often surprised by how many factors influence something as simple as “providing power.” This article outlines the essential concepts behind choosing the right power source, clarifies the often-misunderstood distinction between dedicated power supplies and battery-oriented chargers, and explores how cable design and USB/USB-C standards affect voltage stability and current delivery. By understanding these foundational elements, users can avoid common pitfalls, ensure consistent performance, and prolong the lifespan of their SBC hardware.

# 2. When do i have to consider this?
Whenever you have problems with random reboots, kernel panics, and/or non-working peripherals (especially power hungry devices like spinning hard drives), the first thing you should do is check your power situation. The operating system we deliver is rock-solid if your board has sufficient and reliable power.

> If you got send here please read this article carefully!
{.is-info}


# 3. PSU or Charger? Whats the difference?

The difference between these power bricks lies in their intended usage. A charger is designed to charge a battery, so it does not need to handle brown-outs. Brown-outs occur when the AC voltage of your home drops, which can happen due to various reasons. For example, a refrigerator requires a significant amount of power to start its compressor. When the compressor activates, it may draw so much power from your wall socket that the voltage in your entire home momentarily drops below the standard rated voltage for your country. This situation can cause a charger to temporarily stop supplying power. However, this is not an issue when using the charger to charge a battery-powered device because the device has its own battery to run on. A Single Board Computer (SBC), on the other hand, relies entirely on that power and may crash during a brown-out. 

- This is the voltage of a fridge. You can tell when it did turn on by looking at the voltage drop:
![voltage.png](/psu-charger/voltage.png)

A PSU (Power Supply Unit) is built to manage such situations. It incorporates capacitors that function like small batteries to compensate for brief drops in voltage, providing a stable power source for your SBC. 

## 3.1 How do i find out what kind of power brick i have?

Unfortunately, there isn't a reliable way to determine which type of power brick you have. However, you can make some assumptions to identify it. Generally, since a PSU requires more components, they tend to be heavier and more expensive. This doesn’t mean that an expensive power brick is necessarily a PSU, but you can assume that a cheap or free power brick (such as one that came with your phone) is likely a charger. 


<details>
<summary><b>Recommended Power Supplies</b></summary>
  
  > The links have been included for demonstration purposes only. We received no compensation for including them, nor do we endorse any specific purchasing sources.
{.is-info}
  
We recommend using the [Orange Pi PD100W](http://www.orangepi.org/html/hardWare/powerSuppliesAndCables/details/PD100W-EU.html), which is a 100W USB-C PD-compliant power supply. It did suppried us in how well it is built and handles power delivery. 

Another great option is to purchase a [Lenovo USB-C 65W laptop power supply](https://www.lenovo.com/gb/en/p/accessories-and-software/chargers-and-batteries/chargers/4x20m26276). These can often be found at reasonable prices in the used market and work very well with our supported SBCs. 

A third option is the PSU of an Apple Macbook, as long as you choose the USB-C version of it.
[35 Watts Version](https://www.apple.com/shop/product/mw2h3am/a/35w-dual-usb-c-port-compact-power-adapter)
[70 Watts Version](https://www.apple.com/shop/product/mxn53am/a/70W%20USB-C%20Power%20Adapter)
[140 Watts Version](https://www.apple.com/shop/product/mw2m3am/a/140w-usb-c-power-adapter)
  
The PSU included with the FydeTab Duo is good too; however, it cannot be purchased separately.

[This UGREEN brick](https://eu.ugreen.com/products/ugreen-65w-usb-c-pd-charger-4-ports) is also a good option, as long as you take care of [3.4 What about multi-port chargers](#h-3-4-what-about-multi-port-chargers?)

  
</details>
  
## 3.2 How to determine the power output of my brick?

While most chargers and power supplies advertise their maximum power output, this is not true for all voltages they support. If we examine the Orange Pi PD100W, its specifications are listed on both their product page and on the power brick itself. To determine the power output in watts, you need to multiply voltages by amperes.

<br>

$Voltage * Ampere = Watt$
<div style="display:flex; align-items:flex-start; gap:20px;">

<div style="flex:1;">
  
<br>
  
| Voltage | Ampere | Watt |
| ------- | ------- | ------ |
| 5 Volts | 3 Amperes | 15 Watts |
| 9 Volts | 3 Amperes | 27 Watts |
| 12 Volts | 3 Amperes | 36 Watts |
| 15 Volts | 3 Amperes | 45 Watts |
| 20 Volts | 5 Amperes | 100 Watts |

From this list, we can determine that this brick is capable of powering an Orange Pi 6 Plus, as it requests 20V from the brick, providing up to 100W for use. Its predecessor, the Orange Pi 5 Plus, requests 5V from the brick and receives only 15W with this power supply. This amount is barely sufficient to power this SBC since its chip (RK3588) can draw 15W on its own. Additionally, the product page of the Orange Pi 5 Plus states its power requirement as 5V/4A or 20W.
  
</div>

<img src="/psu-charger/100wpsu.png" style="max-width:350px;">

</div>

## 3.3 What is USB-C Power Delivery and why does it matter?

As shown in the table above, chargers and PSUs that adhere to the USB-C PD standard can offer multiple output voltages. If your power brick, SBC, and cable (more on cables later) all support PD, your devices have the capability to communicate over the USB-C cable to determine acceptable voltages and amperes for both the power brick and the SBC. This communication allows them to select the best possible combination. Not all devices correctly support or implement this feature. For example, the Orange Pi 5 Plus does not support USB-C PD despite using a USB-C port to power the board. In contrast, the Radxa Rock 5/5B supports USB-C PD at 9V/2A, 12V/2A, 15V/2A, and 20V/2A.

Since USB-C Power Delivery is part of the USB-C feature set, it is not supported by USB-A. If USB-C PD communication does not occur, the output voltage from your power brick will be 5 Volts.

> The USB-C PD communication should always occur at 5 Volts, but there are power bricks that have implemented this feature incorrectly. These power bricks might attempt PD communication at the last known voltage, potentially damaging your SBC. Such bricks are rare but do exist.
{.is-warning}

## 3.4 What about multi-port chargers?
Some USB power supplies come with multiple ports, either USB-A or USB-C. As USB-A can only output 5 volts and therefore don't do USB-C PD, those ports are not problematic. However, if your PSU has multiple USB-C ports, the charger must handle USB-C PD for any connected device. 

Most PSUs implement this feature simply: they initiate the USB-C PD process whenever a new device is connected to any port. Therefore, if you're powering your SBC with one port and then connect another device, it will reset power to establish USB-C PD, which in turn resets your SBC as well. Thus, if you plan on using a multi-port brick, avoid connecting new devices while it powers your SBC. 

# 4. Cables; aren't they all the same?

As you might have already guessed, if all cables were the same, this chapter would not exist. USB cables differ in their copper wiring between both plugs, although not the plugs themselves. The following table shows which USB standards are supported by different copper connections.

| USB standard | VCC & GND | Data Plus / Minus | SSTX+ / SSTX− & SSRX+ / SSRX− | CC1 / CC2 | SBU1 / SBU2 | TX1+ / TX1− & RX1+ / RX1− | TX2+ / TX2− & RX2+ / RX2− | GND_DRAIN / Shield | Supported Power |
| ------- | ------- | ------ | ------- | ------- | ------ | ------- | ------- | ------ |
| USB 1.1 & 2.0 | X | X | | | | | | | 2.5 Watts |
| USB 3.x | X | X | X | | | | | X | 15 Watts |
| USB-C minimal | X | X | | X | X | | | | 60 Watts |
| USB-C full | X | X | | X | X | X | | X | 240 Watts |
| USB-C Thunderbolt | X | X | | X | X | X | X | X | 240 Watts |

While the table distinguishes between three types of USB-C cables, it ultimately depends on the manufacturer how much copper they use in their cables. Since copper is expensive, as you might have guessed, many manufacturers cut costs with these cables. Additionally, just because a USB cable has USB-C plugs on both ends doesn't mean it supports any USB-C standard. You can simply manufacture a USB 2.0-compliant cable with USB-C plugs and sell them inexpensively. These types of cables are commonly sold at gas stations, airports, or grocery stores. They typically do not have any ratings printed on their packaging and usually provide only 2.5 watts, similar to "normal" USB 2.0 cables.

> Do not buy this kind of cables! They are slow and have the potential to catch fire!
{.is-warning}


Another aspect to consider is the existence of a so-called "e-marker" chip. This chips holds the information about what capabilities your cable have. Without this chip, a cable can deliver 60 Watts at max. With 30 AWG copper connections, delivering 60 watts can be potentially dangerous; however, neither the power brick nor the SBC will detect this issue. The board might continue drawing 60 watts (if necessary) until the cables catch fire. Cables that have the potenial to catch fire are forbidden in most countries, but that does not stop anyone from selling them.

## 4.1 Does cable length matter?
In an ideal world, a USB-C cable should function perfectly up to a length of 3 meters; however, as demonstrated in the previous chapter, we don't live in such a perfect world. 

Longer cables encounter two primary issues. First, any cable can act as an antenna if not properly shielded, ironically the shielding itself acts like an antenna by redirecting captured signals to ground, so those signals can not affect any internal wires. The longer the cable, the more effectively it functions as an antenna, making good shielding essential for both internal wire pairs and the entire cable. 

The second issue arises from the internal resistance of the copper connections. As previously discussed, manufacturers often reduce costs by omitting some copper connections. Another cost-saving measure is thinning these connections, which increases their internal resistance. This presents two problems: First, continuously drawing high power through thin cables generates heat. If this heat cannot dissipate—for example, if your cable is concealed in a duct—it could eventually lead to fire. The second, more common issue is that increased resistance affects voltage levels. Assuming a cheap cable has a resistance of 0.25 Ω and our SBC operates on 5V/2A, the calculation goes as follows:

$2 A × 0.25 Ω = 0.5 V$

This results in a voltage drop of 0.5 volts. Thus, while the power brick outputs 5 volts, only 4.5 volts reach your SBC. 

The rule of thumb is that the longer your cable, the better its construction must be. It's best to use the shortest cable possible for your setup, but don't exceed 1.5 meters of cable length.

If you really need to exceed 1.5 meters we recommend the use of an [Apple USB-C Cable](https://www.apple.com/shop/product/myqt3am/a/240w-usb-c-charge-cable-2-m).

## 4.2 How to determine which kind of cable i have?

Apart from USB-A cables, which have a blue plug if they support USB 3 and any other color for USB 1.X or 2.0, there are only two ways to determine how they are constructed. 

The simplest, but destructive, method is to peel away the cable's shielding and count the copper connections between both ends. If done carefully, the cable might still function afterward; however, since USB-C is designed for high-speed and high-frequency applications, this isn't guaranteed. 

Another method is to use a cable tester. These can be found inexpensively on platforms like AliExpress. Typically, you plug in both ends of your cable into the tester, and its LEDs will light up to indicate any copper connections present in the cable. 

Neither of these methods can be performed in-store or if purchasing online. As a rule of thumb, check for ratings on the package or product page. Additionally, when buying cables at a local store, you can gauge their quality by feeling how stiff they are. Generally, more stiffness indicates better shielding and more copper connections inside the cable. At minimum, avoid purchasing the cheapest cables available or you will be disappointed.

> The Youtube channel "GreatScott!" has made a great two part series about USB-C cables found [here (Part one)](https://www.youtube.com/watch?v=ZikvlsVDiQY) and [here (Part two)](https://www.youtube.com/watch?v=LOIVrVVYBfA).
{.is-info}

# 5. What to do with all this information?

After reading all of this, you might conclude that this is quite complicated. You're correct! If you encounter issues as described in the section "2. When do I have to consider this?", check the product pages for your SBC, power brick, and cable. If you can't find any information about ratings, stop using that power brick or cable with your SBC. 

If you read this article before purchasing a PSU, think about how you'll use your board. For instance, if you want to use an Orange Pi 5 Plus with two spinning hard drives rated at 5V/1A each, simply add those values:

$20W+5W+5W=30W$

Then, to ensure your power brick operates efficiently without being overburdened, calculate how much power it should provide so that its usage is around 80% normally:

$30W / 0.8 =37.5W$

In this case, we recommend a PSU rated at a minimum of 37.5 watts. 

> TL;DR Get the specifications, do the math and don't use cheap cables!
{.is-success}
