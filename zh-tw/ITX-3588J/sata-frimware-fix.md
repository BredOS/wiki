---
title: Sata Firmware Fix
description:
published: false
date: 2025-09-12T09:18:06.486Z
tags:
editor: markdown
dateCreated: 2025-09-12T09:18:06.486Z
---

# SATA Firmware Fix

### 1. Prerequisites

- A CH341A-based flasher
- Either a soldering iron or an SPI clip
- The new firmware file (download it from [here])
- Another device with Linux installed (Windows should work too, but is not covered here)

A very handy pack including the flasher, clip, and other useful accessories can be ordered here:
https://www.aliexpress.com/item/32263275388.html

### 2. Connect to SPI

> ⚡ _Before connecting anything to power, double-check that all connectors are correctly oriented!_ ⚡
> {.is-warning}

The simplest way to connect to the SPI chip is by using the clip. It can be a bit tricky to get a firm connection, but it doesn't require any soldering skills or tools. Additionally, using the clip is very unlikely to cause any damage to the board.

On the other hand, if you have soldering experience, it's not a difficult task to desolder and resolder the eight pins of the SPI chip.

The SPI chip is located near the SATA ports, right next to the mSATA slot. Look for the square chip labeled "JMB575" — that's the SATA controller. Next to it, you'll find a smaller 8-pin chip labeled "W25X40CL", which is the SPI chip. The label on the SPI chip can be hard to read, but once you've located the SATA controller, it should be easy to identify the SPI chip.

#### 2.1 Connect the Clip

Pin 1 on the clip is color-coded on the cable — the red wire indicates it. The red wire should face the edge of the board where the SATA ports are located.
Make sure the clip is fully inserted. If it's connected correctly, you should be able to lift the board using the clip.

Connect the other end of the cable to the flasher. The correct orientation is as follows: if the USB connector of the flasher is pointing away from you, the cable should go into the upper four holes, with the red wire in the bottom right corner.

#### 2.2 Or desolder the SPI Chip

Grab some soldering wick and flux, heat up your iron, and desolder the chip. You should know what you're doing!

You can then either solder the chip directly onto the flasher (there’s a pad on the back of the flasher for this), or use one of the adapter boards included in the pack mentioned above.

Pin 1 is marked on the chip with a small dot and is labeled with a "1" on the flasher or adapter board.

### 3. Flash Firmware

First you need to install flashrom.

```
sudo pacman -S flashrom
```

#### 3.1 Backup Firmware

Before we begin flashing a new rom its a good idea to backup the existing rom. Whenever something goes wrong you're able to go back with this file


