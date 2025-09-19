---
title: Sata固件修复
description:
published: true
date: 2025-09-19T05:01:28.982Z
tags:
editor: markdown
dateCreated: 2025-09-12T09：18：06.486Z
---

# 1. 必备条件

- 基于 CH341A 的闪光器
- 或是一根吸铁片段或 SPI 素材
- 新的固件文件 (从 [here](/wiki-itx3588j-pics/satafw/sata_adapter_en25f40.bin) 下载)
- 已安装Linux的另一台设备 (window也应该正常工作，但不在这里覆盖)

这里可以订购一个非常便捷的包，包括烧录机、片段和其他有用的配件：
https://www.aliexpress.com/item/3226327388.html
[spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)

> 如果链接已过期，请随时在 Discord 或 Telegram 上给我们头部。

# 2. 连接到SPI

> _Before connecting anything to power, double-check that all connectors are correctly oriented!_
> {.is-warning}

连接到SPI 芯片的最简单方式是使用片段。 获得一个固定连接可能有点微妙，但它不需要任何焊接的技能或工具。 此外，使用剪切极不可能对董事会造成任何损害。

另一方面，如果你有沉浸的经历，要去除和解析SPI芯片的八个粉丝并不是一个困难的任务。

- SPI 芯片位于SATA 港口附近，紧靠mSATA 槽旁。 SPI 芯片位于SATA 港口附近，紧靠mSATA 槽旁。 寻找标题为“JMB575”的方块芯片——这是SATA控制器。 接下来, 你会找到一个更小的 8 pin 芯片，标签为“W25X40CL”，也就是SPI 芯片。 SPI 芯片上的标签可能难以读取， 但一旦你找到了 SATA 控制器，它应该很容易识别SPI 芯片。
  ![sata-controller-text-scaled.jpg](/wiki-itx3588j-pics/sata-controller-text-scaled.jpg) 接下来, 你会找到一个更小的 8 pin 芯片，标签为“W25X40CL”，也就是SPI 芯片。 SPI 芯片上的标签可能难以读取， 但一旦你找到了 SATA 控制器，它应该很容易识别SPI 芯片。

![sata-controller-text-scaled.jpg](/wiki-itx3588j-pics/sata-controller-text-scaled.jpg)

## 2.1 连接片段

片段上的Pin 1在线上是颜色编码的——红线表示它。 红线应面临SATA港口所在的船上的边缘。

- 确保素材已完全插入. 如果它连接正确，你应该能够使用片段取消看板。

如果它连接正确，你应该能够使用片段取消看板。
![spi-clip-connected-cut.jpg](/wiki-itx3588j-pics/spi-clip-connected-cut.jpg)

- 将电缆的另一端连接到烧录器。 正确的方向如下：如果飞行器的 USB 连接器指向您。 电缆应该进入下面的四个洞，左上角的红线应该是红线。

![flasher-clip-connected-cut-scaled.jpg](/wiki-itx3588j-pics/flasher-clip-connected-cut-scaled.jpg)

## 2.2 或去除SPI芯片

拿起一些卷起的狼和流感，加热你的铁，去除芯片。 你应该知道你在做什么！ 你应该知道你在做什么！

然后你就可以把芯片直接放到平面上(在平面背面上有一个平面)，然后你就可以把它放到平面上， 或使用上面提到的包中包含的适配板之一。
应该有一个没有人居住的委员会和ZIF套接字作为包的一部分。 选择明智。

- Pin 1在芯片上用一个小点标记，并在平面板或适配器板上贴上"1"标签。

![zif-socket-cut-scaled.jpg](/wiki-itx3588j-pics/zif-socket-cut-scaled.jpg)

- 或

![spi-soldered-cut.jpg](/wiki-itx3588j-pics/spi-soldered-cut.jpg)

## 2.3 检查连接

- 首先你需要安装 flashrom。

```
sudo pacman -S flashrom
```

> 确保你的火焰被设置为3.3伏！
> {.is-warning}

检查所有电缆并确保您的 ITX-3588J 板在使用片段时断电。
然后连接到您的Linux设备并运行以下命令。
如果它报告了上述SPI芯片的名字，你很乐意去做。
然后连接到您的Linux设备并运行以下命令。

- 如果它报告了上述SPI芯片的名字，你很乐意去做。

```
sudo flashrom -p ch341a_spi --flash-name
```

```
flashrom 1.4.0-devel (git:v1.2-1355-g9ccbf1cf) 在 Linux 6.15.7-1-BredOS (x86_64)
flashrom 是免费软件，获得源代码在 https://flashrom。 rg

在延迟循环中使用时钟时间(clk_id：1，分辨率：1ns).
在ch341a_spi上找到Winblel flash chip "W25X40" (512 kB，SPI)。
```

如果没有，请检查素材的连接或检查您的嵌入工作，并验证所有连接器的方向。

# 3. 闪光固件

## 3.1 备份旧固件

在刷新一个新的ROM之前，支持现有的ROM是一个好主意。
如果出现任何错误，您将能够使用这个备份恢复它。
如果出现任何错误，您将能够使用这个备份恢复它。

- 用以下命令转储闪存：

```
sudo flashrom -p ch341a_spi -r firmware_dump.bin
```

- 然后再次转储它并比较两个文件，以确保正确传输数据。

```
sudo flashrom -p ch341a_spi -r firmware_dump-1.bin
diff firmware_dump.bin firmware_dump-1.bin
```

如果“diff”不产生输出, 你就好了。
如果确实如此，请检查素材的连接或检查您的焊接工作，并验证所有连接器的方向。
如果确实如此，请检查素材的连接或检查您的焊接工作，并验证所有连接器的方向。

## 3.2 刷新新固件

- 正如标题所表明的那样简单：

```
sudo flashrom -p ch341a_spi -w sata_adapter_EN25F40.bin 
```

```
flashrom 1.4.0-devel (git:v1.2-1355-g9ccbf1cf) on Linux 6.15.7-1-BredOS (x86_64)
flashrom is free software, get the source code at https://flashrom.org

Using clock_gettime for delay loops (clk_id: 1, resolution: 1ns).
Found Winbond flash chip "W25X40" (512 kB, SPI) on ch341a_spi.
===
This flash part has status UNTESTED for operations: WP
The test status of this chip may have been updated in the latest development
version of flashrom. If you are running the latest development version,
please email a report to flashrom@flashrom.org if any of the above operations
work correctly for you with this flash chip. Please include the flashrom log
file for all operations you tested (see the man page for details), and mention
which mainboard or programmer you tested in the subject line.
Thanks for your help!
Reading old flash chip contents... done.
Erase/write done from 0 to 7ffff
Verifying flash... VERIFIED.
```

如果您看到文本"VERIFIED"，固件已被正确刷入。 如果你使用了片段，简单地断开它的连接，你很好。 如果你去除芯片，你知道要做什么。 如果你使用了片段，简单地断开它的连接，你很好。 如果你去除芯片，你知道要做什么。

> 所有的 SATA 端口都应该很好的工作！
> {.is-success}
