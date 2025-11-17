---
title: 设备树
description:
published: true
date: 2025-11-17T09:34:50.502Z
tags:
editor: markdown
dateCreated: 2024-11T11:50:39.940Z
---

# 1. 简介

设备树是一种描述ARM和RISC-V系统通常使用的硬件的机制。 允许内核在不改变内核驱动程序代码的情况下发现和配置硬件设备。
与x86系统不同的是，ACPI表格使得自动硬件发现和配置成为可能。 大多数ARM 系统需要修改设备树才能声明硬件更改。 它们分成两种设备树类型，基础和叠加层。 虽然设备树基础描述了您的SBC的全部硬件，并且叠加层仅用于改变它的特定部分。
与x86系统不同的是，ACPI表格使得自动硬件发现和配置成为可能。 大多数自动取款机和RISC-V系统需要修改设备树才能声明硬件变更。

# 2. 设备树

## 在 UEFI 和 Grub 系统中切换设备树

打开 grub 配置文件 `/etc/default/grub` 。
打开 grub 配置文件 `/etc/default/grub` 。
找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：
打开 grub 配置文件 `/etc/default/grub` 。
找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：
打开 grub 配置文件 `/etc/default/grub` 。
找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：

- 打开 grub 配置文件 `/etc/default/grub` 。
  找到以 `GRUB_DTB=` 开头的行，并将路径添加到设备树文件，例如：

```bash
GRUB_DTB= dtbs/rockchip/xxx.dtb
```

- 然后更新grub 配置：

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

> 只能指定一个 DTB
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

## Updating Device Trees in U-Boot systems with extlinux

- 编辑 extlinux 配置文件 `/boot/extlinux/extlinux.conf` 。 使用 fdt\`, 例如: 使用 fdt`, 例如: 使用 fdt\`, 例如: 使用 fdt`, 例如: 使用 fdt\`, 例如:

```bash
fdt /dtbs/rockchip/xxx.dtb
```

然后编辑以匹配您的设备树路径。 保存并重启您的系统。 保存并重启您的系统。 保存并重启您的系统。 保存并重启您的系统。 保存并重启您的系统。

> 只能指定一个 DTB
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}
> {.is-info}

# 4. 生成设备树覆盖

> 在继续本篇文章之前，请考虑审查[如何启用 DTBOs](/how-to/how-to-enable-dtbos)。
> {.is-info}

在这个示例中，我们生成一个叠加层，使两个GPIO-Pins 上的 I2C 能够与一个 BMP280 传感器进行通信。

- 创建叠加层源文件：

```
nano rk3588-bmp280.dts
```

- 并将你的 dt 源的内容放入其中。 我们使用 BMP280的示例代码：

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

- 将 dt 源编译为二进制格式：

```
dtc -I dts -O dtb rk3588-bmp280.dts -o rk3588-bmp280.dtbo
```

- 然后移动二进制文件到您的叠加层文件夹：

```
mv rk3588-Bmp280.dtbo /boot/dtbs/rockchip/overlay/
```

> 要启用设备树叠加层 [编辑 extlinux 配置] (/how-to/how-to-enable-dtbos#h-4-1-edit-the-extlinux-configuration) for u-booted based systems 或 [配置 UEFI] (/how-to/how-to-enable-dtbos#h-3-4-configure-uefi) 用于基于 UEFI 的系统。
> {.is-info}

## 3.1 验证设备树叠加层已按预期加载

- 检查内核模块是否加载：

```
lsmod | grep bmp280
```

- 输出应该列出模块。

```
bmp280_spi             16384  0
bmp280_i2c             16384  0
bmp280                 28672  2 bmp280_i2c,bmp280_spi
```

> 请注意，i2c和spi两种支持都显示可用，这是因为bmp280传感器同时支持SPI和i2c接口。  然而，就这个例子而言，只适用i2c支持。
> {.is-info}

- 检查是否可以在 I2C 界面检测到 BMP280 。

```
i2csection -y 8
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

> 请注意，i2c8大客车上地址0x76的值已经从'76'改为'UU'，这是预期和想要的； 它表明本机内核mp280 支持已经取得了传感器的所有权。
> {.is-info}

- 检查内核日志是否显示设备：

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

- 从 BMP280 传感器查询温度：

```
cat /sys/devices/platform/feca00.i2c/i2c-8/8-0076/iio:device1/in_temp_input
```

```
输出：30630

温度 30.630 摄氏度
```

- 从 BMP280 传感器查询压力：

```
cat /sys/devices/platform/feca0000.i2c/i2c-8/8-0076/iio:device1/in_presence_input
```

```
输出：100.292183593

返回的压力以千帕为单位。
```
