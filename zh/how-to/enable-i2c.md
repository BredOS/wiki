---
title: 启用 I2C 接口
description:
published: false
date: 2025-11-18T07:56.994Z
tags:
editor: markdown
dateCreated: 2025-11-17T10:52：11.550Z
---

# 2. 介绍信息

可以按照两项基本战略启用和使用i2c支助。  首先，仅启用i2c接口。 然后使用各种脚本和/或编程语言与传感器通信，使用i2c公共汽车和协议。  第二，如果可用，则使用本机操作系统传感器支持，即： 一个内核级别的驱动程序，通过i2c公共汽车和协议再次与传感器通信。  i2c 协议参考 https://en.wikipedia.org/wiki/I%C2%B2C

利用i2c接口和通信协议的设备类型包括传感器、显示屏幕、触摸板等。  具体到这个示例，将支持流行的 bmp280 温度和压力组合传感器。  见 https://www.bosch-sensortec.com/products/environmental-sensors/presure-sensors/bmp280/。

# 3. 我应该使用哪种类型的支持？

有各种图书馆为mp280传感器提供直接支持。  例如，Adafruit提供了python兼容的 bmp280 传感器支持，请参阅https://learn.adafruit.com/welcometo-circuitpython/couritpython库和 https://learn.adafruit.com/adafruit-bmp280-barometric-los-plus-temature-sensor-breakout/cleitpython-test。 支持本机内核。 设备树方法可以用来告诉内核有一个设备，并让它接管它的控制权。

> To enable native kernel support we must create a device tree overlay like described in [Creating an device tree overlay from scratch](/development/device-trees#h-3-creating-an-device-tree-overlay-from-scratch)
> {.is-info}

# 4. Wiring

- 这是最多的 RK3588 设备 GPIO 布局。 请参阅您特定设备的文档以供引脚布局！| Typical RK3588 GPIO Pin Layout                                          |
  | ----------------------------------------------------------------------- |
  | ![gpio-pin-layout.png](/enable-i2c/gpio-pin-layout.png) |

- 要将您的传感器连接到I2C，就像在本图中显示的那样：

### Tabset {.tabset}

#### I2C Bus M0

\| 传感器Pin| GPIO 功能 | GPIO Pin| 在棋盘上粘贴颜色 | 图表上粘贴颜色 |
\| ---------- | ------------ | ------ | ------ |
\| VCC | 3. v|GPIO Pin 1 | Yellow | Red |
\| GND | GND | 任何地面，例如 GPIO Pin 9 | Blue |
\| SDA | i2c SDA (数据) | GPIO Pin 3 | Blue | Pink |
\| SCL | i2c SCL (时钟) | GPIO Pin 5 | Blue | Pink |

#### I2C Bus M2

\| 传感器Pin| GPIO 功能 | GPIO Pin| 在棋盘上粘贴颜色 | 图表上粘贴颜色 |
\| ---------- | ------------ | ------ | ------ |
\| VCC | 3. v|GPIO Pin 1 | Yellow | Red |
\| GND | GND | 任何地面，例如 GPIO Pin 9 | Blue |
\| SDA | i2c SDA (数据) | GPIO Pin 37 | Blue | Pink |
\| SCL | i2c SCL (时钟) | GPIO Pin 12 | Blue | Pink |

#### I2C Bus M3

\| 传感器Pin| GPIO 功能 | GPIO Pin| 在棋盘上粘贴颜色 | 图表上粘贴颜色 |
\| ---------- | ------------ | ------ | ------ |
\| VCC | 3. v|GPIO Pin 1 | Yellow | Red |
\| GND | GND | 任何地面，例如 GPIO Pin 9 | Blue |
\| SDA | i2c SDA (数据) | GPIO Pin 15 | Blue | Pink |
\| SCL | i2c SCL (时钟) | GPIO Pin 16 | Blue | Pink |

#### I2C Bus M4

\| 传感器Pin| GPIO 功能 | GPIO Pin| 在棋盘上粘贴颜色 | 图表上粘贴颜色 |
\| ---------- | ------------ | ------ | ------ |
\| VCC | 3. v|GPIO Pin 1 | Yellow | Red |
\| GND | GND | 任何地面，例如 GPIO Pin 9 | Blue |
\| SDA | i2c SDA (数据) | GPIO Pin 11 | Blue | Pink |
\| SCL | i2c SCL (时钟) | GPIO Pin 13 | Blue | Pink |

###

> 请仔细检查您面板上的引脚布局。 一个错误的有线传感器可能无法正常工作，甚至可能被损坏而无法修复！
> {.is-info}

# 5. 检查连接到哪个i2c总线？

- 安装 i2c-tools 包。i2c-tools 包提供CLI 命令，列出在 i2c 大客车上找到的传感器。

```
pacman -Sy i2c-tools
```

```
ls -l /dev/i2c*
```

请注意，i2c-8大客车默认不存在。  专门适用于 IndieDroid 的 i2c 总线 8 (m2)，默认情况下未启用， 但可在GPIO Board pins 3 and 5, respectively i2c SDA (i). 。数据引导和i2c SCL(即时钟固定)。

> 无论使用完整的本机内核支持，还是仅启用适用的 i2c 大客车， 需要使用设备树源文件来验证 i2c 公交功能。  这将确保正确的公共汽车上的 i2c 接口具有功能，传感器可在预期的i2c 地址找到。
> {.is-info}

查找设备树源文件以启用 i2c bus 8...  通过 GPIO 头上的 InidedDroid Nova i2c 支持通过 pin 3 和 5, i。 e. i2c SDA (data pin) 和 i2c SCL (count pin), 并且被限定为“m2”变量。  因此，必须修改引导配置以载入编译的 rk3588-i2c8-m2 设备树文件。

通过 Secure Shell (SSH) 或桌面(GUI) 打开终端会话并升到根级访问...

```
苏文
```

确认 GPIO i2c 8 (m2) 设备树对象文件存在于引导分区...

```
查找/boot | grep i2c8
```

输出看起来就像这样了

```
/boot/dtbs/rockchip/overlay/rk3588-i2c8-m2.dtbo
/boot/dtbs/rockchip/overlay/rk3588-i2c8-m4.dtbo
```

重启 IndieDroid Nova...

```bash
reboot
```

## 4. 验证 i2c 公共汽车现在可见

```bash
ls -l /dev/i2c* | grep i2c-8
```

```
crw-rw---- 1 root i2c 89, 8 Sep 22 09:44 /dev/i2c-8
```

如果上面的设备目录不存在，那么编译后的设备树文件就没有像预期的那样加载。  验证`extlinux.conf`文件已根据需要更改，以启用i2c 8 bus，使用文件的`m2`变量。  例如...

```
fdtoverlays /dtbs/rockchip/overlay/rk3588-i2c8-m2.dtbo
```

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
70: -- -- -- -- -- -- 76 --
```

> bmp280传感器应出现在i2c总线8上，地址0x76。 如上文70行和6栏中提到的“76”所示。  如果情况不是这样，那么设备树文件会按预期加载，因此传感器不会在 i2c bus 8 上显示。  如果计划仅启用适用的 i2c 公共汽车，即： 8. 除了安装应用程序级库和开发传感器查询适用代码外，不需要采取其他步骤。  如果需要对传感器使用完整的本机内核支持，请完成以下步骤。
> {.is-info}