---
title: Extended Flashing Guide
description: A bit more on how to use RKDevelopTool
published: true
date: 2025-09-28T13:02:34.069Z
tags: 
editor: markdown
dateCreated: 2025-09-28T13:02:13.948Z
---

Well, you just want more progress bars in your life, right?
We gotya covered :thumbsup: don't worry.

## Reading chosen flash medium info
 - `sudo rkdeveloptool rfi`
 
This command will show you what is the chosen flash medium that is going to be flashed.
By default, this usually is the eMMC, unless it's unavailable.

```
[bill88t@prion | ~/Downloads]> sudo rkdeveloptool rfi
Flash Info:
	Manufacturer: SAMSUNG, value=00
	Flash Size: 14910 MB
	Flash Size: 30535680 Sectors
	Block Size: 512 KB
	Page Size: 2 KB
	ECC Bits: 0
	Access Time: 40
	Flash CS: Flash<0>
```

## Changing flash target
Want to flash / dump not the eMMC but a different thing?

`sudo rkdeveloptool cs 2` to choose the sdcard.
`sudo rkdeveloptool cs 9` to select the SPINOR chip.
`sudo rkdeveloptool cs 1` to select the eMMC again.

The change will be shown in `sudo rkdeveloptool rfi`.