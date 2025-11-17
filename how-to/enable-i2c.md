---
title: Enable I2C Interface
description: 
published: false
date: 2025-11-17T12:09:29.224Z
tags: 
editor: markdown
dateCreated: 2025-11-17T10:52:11.550Z
---

# 1. Introduction


The i2c support can be enabled and used according to two basic strategies.  First, is enable of the i2c interface alone, and then use various scripting and/or programming languages to communicate with the sensors on the using the i2c bus and protocol.  Second, when available, use the native operating system sensors support, i.e. a kernel level driver, to communicate with the sensors again via the via the i2c bus and protocol.  Reference for the i2c protocol https://en.wikipedia.org/wiki/I%C2%B2C

The types of devices which leverage the i2c interface and communication protocol include, sensors, display screens, touch panels, etc., is extensive.  Specific to this example, will be establishing support for the popular bmp280 temperature and pressure combined sensor.  Reference https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp280/.


# 2. What type of support should i use? 

There are various libraries that provide direct support for the bmp280 sensor.  For example, Adafruit, provides python compatible bmp280 sensor support, refer to https://learn.adafruit.com/welcome-to-circuitpython/circuitpython-libraries and https://learn.adafruit.com/adafruit-bmp280-barometric-pressure-plus-temperature-sensor-breakout/circuitpython-test. For full native kernel support, the device tree method can be used to tell the kernel that there is a device and to let it take over control of it. 

> To enable native kernel support we must create a device tree overlay like described in [Creating an device tree overlay from scratch](/development/device-trees#h-3-creating-an-device-tree-overlay-from-scratch)
{.is-info}

# 3. Wiring

![gpio-pin-layout.png](/enable-i2c/gpio-pin-layout.png)
| Sensor Pin | GPIO Function | GPIO Pin | Pin Color | 
| ---------- | ------------- | -------- | -------- |
| VCC | 3.3v | GPIO Pin 1 | Yellow |
| GND | GND | Any Ground such as GPIO Pin 9 | Black |
| SDA | i2c SDA (data) | GPIO Pin 3 | Blue | 
| SCL | i2c SCL (clock) | GPIO Pin 5 | Blue |




# 4. Check to which i2c bus is the sensor connected?

- Install i2c-tools package, The i2c-tools package provides CLI commands to list the sensors found on the i2c bus.

```
pacman -Sy i2c-tools
```

```
ls -l /dev/i2c*
```

Note that the i2c-8 bus is not present by default.  Specific to the IndieDroid the i2c bus 8 (m2), which is not enabled by default, but available on GPIO board pins 3 and 5, respectively i2c SDA (i.e. data pin), and i2c SCL (i.e. clock pin).

> Regardless of using full native kernel support, or only enablement of the applicable i2c bus, the use of a device tree source file to validate the i2c bus function is required.  This ensures that the i2c interface on the correct bus is functional, and the sensor is found at the expected i2c address.
{.is-info}




Find the device tree source file to enable i2c bus 8..  Specific to the InideDroid Nova i2c support on the GPIO header via board pins 3 and 5, i.e. i2c SDA (data pin) and i2c SCL (clock pin), and are qualified as the 'm2' variant.  Thus the boot configuration must be amended to load compiled rk3588-i2c8-m2 device tree file.

Open a terminal session via Secure Shell (SSH) or within the desktop (GUI) and elevate to root level access...

```
su
```
Confirm that the GPIO i2c 8 (m2) device tree object files are present on the boot partition...

``` 
find /boot | grep i2c8
```
Output will look something like this
```
/boot/dtbs/rockchip/overlay/rk3588-i2c8-m2.dtbo
/boot/dtbs/rockchip/overlay/rk3588-i2c8-m4.dtbo
```

Reboot the IndieDroid Nova...

```bash
reboot
```

## 5. Validate i2c bus is now visible

```bash
ls -l /dev/i2c* | grep i2c-8
```

```
crw-rw---- 1 root i2c 89,  8 Sep 22 09:44 /dev/i2c-8
```

Should the above device directory not exist, then the compiled device tree file did not load as expected.  Validate that the `extlinux.conf` file was changed as required to enable the i2c 8 bus, using the `m2` variant of the file.  For example...

```
fdtoverlays /dtbs/rockchip/overlay/rk3588-i2c8-m2.dtbo
```

```
i2cdetect -y 8
```

```
    0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- 76 --
```
> 
> The bmp280 sensor should appear on the i2c bus 8 at address 0x76, as noted by the '76' reference above in the 70 row and 6 column.  Should this not be the case, then the device tree file loaded as expected, thus the sensor is not visible on i2c bus 8.  If planning to only enable the applicable i2c bus, i.e. 8, no more additional steps are required, other than installing the application level libraries and development of sensor query applicable code.  If use of full native kernel support for the sensor is desired, complete the following steps below.
{.is-info}