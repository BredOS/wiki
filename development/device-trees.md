---
title: Device Trees
description: 
published: true
date: 2025-11-17T09:53:51.898Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:50:39.940Z
---

# 1. Introduction
Device trees is a mechanism for describing hardware commonly used in ARM and RISC-V systems, allowing the kernel to discover and configure hardware devices without changing the kernel driver code. They split into two device tree types, base and overlay. While the device tree base describes the entire hardware of your SBC and overlays are used to alter only specific parts of it. 
Unlike x86 systems, where the ACPI tables enable automatic hardware discovery and configuration, most ARM and RISC-V systems need to have their device tree modified to declare hardware changes.

# 2. Switching Device Trees
## 2.1 Switching Device Trees in UEFI and Grub systems
Open the grub configuration file `/etc/default/grub`.
- Find the line that starts with `GRUB_DTB=` and add the path to the device tree file, for example:

```bash
GRUB_DTB= dtbs/rockchip/<your device tree here>.dtb
```


- Then update the grub configuration:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
> There can only be one DTB specified.
{.is-info}


## 2.2 Updating Device Trees in U-Boot systems with extlinux
- Edit the extlinux configuration file `/boot/extlinux/extlinux.conf`. Find the line with `fdt`, for example:

```bash
fdt /dtbs/rockchip/<your device tree here>.dtb
```
Then edit it to match your device tree path. Save and reboot your system.

> There can only be one DTB specified.
{.is-info}


# 3. Creating an device tree overlay from scratch

> Please consider reviewing [How to enable DTBOs](/how-to/how-to-enable-dtbos) before proceeding with this article.
{.is-info}

In this example we generate an overlay that enables I2C on two GPIO-Pins to communicate with an BMP280 sensor.

- Create a overlay source file with:
```
nano rk3588-bmp280.dts
```

- And place the contents of your dt source into it. We use this example code for the BMP280:
```c
/dts-v1/;  // Specifies the version of the Device Tree Source (DTS) format being used
/plugin/;  // Marks this file as a Device Tree overlay plugin

/ {
    metadata {  // Metadata block containing information about this overlay
        title = "Enable BMP280 on I2C8-M2";  // Human-readable title for this overlay
        compatible = "rockchip,rk3588";  // Specifies the SoC this overlay is compatible with
        category = "misc";  // Categorizes the type of overlay
        exclusive = "GPIO1_D6", "GPIO1_D7";  // Pins that this overlay exclusively uses
        description = "Enable BMP280 on I2C8-M2. Pin 3 and 5";  // Detailed description of what this overlay does
    };
};

&i2c8 {  // Reference to the I2C8 controller node in the base device tree
    status = "okay";  // Enable this I2C controller
    pinctrl-names = "default";  // Name of the pin control configuration to use
    pinctrl-0 = <&i2c8m2_xfer>;  // Reference to the pin configuration for this I2C bus
    clock-frequency = <400000>;  // Set I2C clock frequency to 400 kHz (fast mode)
    #address-cells = <1>;  // Number of cells to represent child node addresses
    #size-cells = <0>;  // Number of cells to represent size of child nodes (0 for I2C devices)

    bmp280: bmp280@76 {  // Define a child device node for the BMP280 sensor at I2C address 0x76
        compatible = "bosch,bmp280";  // Device compatible string for BMP280 driver
        reg = <0x76>;  // I2C address of the BMP280 device
        status = "okay";  // Enable this device
    };
};

```

- Compile the dt source to a binary format:

```
dtsc -I dts -O dtb rk3588-bmp280.dts -o rk3588-bmp280.dtbo
```

- Then move the binary to your overlay folder:

```
mv rk3588-bmp280.dtbo /boot/dtbs/rockchip/overlay/
```

> To enable the device tree overlay follow [Edit the extlinux configuration](/how-to/how-to-enable-dtbos#h-4-1-edit-the-extlinux-configuration) for u-boot based systems or [Configure UEFI](/how-to/how-to-enable-dtbos#h-3-4-configure-uefi) for UEFI based system.
{.is-info}


## 3.1 Validate device tree overlay has been loaded as expected

- Check if the kernel module is loaded with:
``` 
lsmod | grep bmp280
```

- The output should list the module.
```
bmp280_spi             16384  0
bmp280_i2c             16384  0
bmp280                 28672  2 bmp280_i2c,bmp280_spi
```
> Note the that both the i2c and spi support shows available, this is because the bmp280 sensor supports both SPI and i2c interfaces.  However, for this example, only the i2c support is applicable.
{.is-info}

- Check if the BMP280 is detectable over the I2C interface.
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
70: -- -- -- -- -- -- UU --
```

> Note that the value at address 0x76 on the i2c 8 bus, has changed from '76' to 'UU', this is expected and desired, in that it shows that the native kernel bmp280 support has taken ownership of the sensor.
{.is-info}

- Check if kernel log shows the device:
```
dmesg | grep bmp280
```
```
[   11.513718] bmp280 8-0076: Looking up vddd-supply from device tree
[   11.513728] bmp280 8-0076: Looking up vddd-supply property in node /i2c@feca0000/bmp280@76 failed
[   11.513757] bmp280 8-0076: supply vddd not found, using dummy regulator
[   11.513830] bmp280 8-0076: Looking up vdda-supply from device tree
[   11.513836] bmp280 8-0076: Looking up vdda-supply property in node /i2c@feca0000/bmp280@76 failed
[   11.513847] bmp280 8-0076: supply vdda not found, using dummy regulator
[   11.694189] SPI driver bmp280 has no spi_device_id for bosch,bmp085
```

- Query temperature from the BMP280 sensor:

```
cat /sys/devices/platform/feca0000.i2c/i2c-8/8-0076/iio:device1/in_temp_input
```
```
Output: 30630

Temperature 30.630 Celsius
```

- Query pressure from the BMP280 sensor:

```
cat /sys/devices/platform/feca0000.i2c/i2c-8/8-0076/iio:device1/in_pressure_input
```
```
Output: 100.292183593

Pressure returned is in kPa units.
```
