---
title: 如何赋予您的SBC 权力
description:
published: true
date: 2025-11-26T07:21:39.068Z
tags:
editor: markdown
dateCreated: 2025-11-24T08:13:30.345Z
---

# 2. 介绍信息

为单一委员会计算机提供可靠的动力是朝着建立稳定有效的嵌入系统迈出的重要一步。 然而，新来者往往感到吃惊的是，有多少因素影响到“提供权力”这种简单的东西。 该条概述了选择正确电源的基本概念，澄清了常常被误解的专用电源和专用电源之间的区别， 并探索电缆设计和USB/USB-C标准如何影响电压稳定性和电流投射。 通过了解这些基本元素，用户可以避免常见的陷井，确保性能一致，并延长其SBC硬件的寿命。

# 1. 我何时必须考虑这一点？

当您有随机重启时出现问题时，内核恐慌， 和/或不起作用的外围设备(尤其是饥饿的电源设备，如硬盘驱动器)，您应该做的第一件事就是检查您的电源。 如果你的棋盘有足够和可靠的能量，我们提供的操作系统是岩石坚固的。

> If you got send here please read this article carefully!
> {.is-info}

# 4. PSU 或充电？ 难道不同吗？

这些电源砖之间的区别在于它们的预定用途。 充电器的设计是为了充电，因此它不需要处理浏览器。 当您家中掉落的交流电压可能由于各种原因而发生浏览。 例如，制冷器需要相当大的能量才能启动其压缩机。 当压缩机激活时， 它可以从你的墙套接字中抽取太多的电力，使你整个家中的电压暂时降到低于你国家的标准额定电压。 这种情况可能导致充电器暂时停止供电。 然而，当使用充电器向电池驱动设备充电时，这不是问题，因为设备有自己的电池可以运行。 另一方面，单一委员会计算机完全依靠这一权力，可能在浏览时崩溃。

- 这是边缘电压。 You can tell when it did turn on by looking at the voltage drop:
  ![voltage.png](/psu-charger/voltage.png)

为了管理这种情况，已经建立了一个PSU（电力供应股）。 它含有像小型电池这样起作用的电容器，以弥补电压中的短暂滴，为您的SBC提供稳定的电源。

## 3.1 我如何找出什么样的动力砖？

不幸的是，无法可靠地确定你拥有哪种类型的电源砖。 然而，你可以作出一些假设来确定它。 一般来说，由于PSU需要更多的组件，它们往往更加沉重和更加昂贵。 这并不意味着昂贵的电源砖必然是一个PSU, 但你可以假设一个廉价或免费的电源砖(例如带着你的手机的电源)可能是充电器。

<details><summary><b>Recommended Power Supplies</b></summary>

> The links have been included for demonstration purposes only. We received no compensation for including them, nor do we endorse any specific purchasing sources.
> {.is-info}

We recommend using the [Orange Pi PD100W](http://www.orangepi.org/html/hardWare/powerSuppliesAndCables/details/PD100W-EU.html), which is a 100W USB-C PD-compliant power supply. It did suppried us in how well it is built and handles power delivery.

另一个很好的选项是购买[Lenovo USB-C 65W 笔记本电脑供电](https://www.lenovo.com/gb/en/p/accessories-and-software/chargers-and-batteries/chargers/4x20m26276)。 在使用过的市场上常常能够以合理的价格找到这些技术，并且与我们支持的附属机构非常有效。

A third option is the PSU of an Apple Macbook, as long as you choose the USB-C version of it.
[35 Watts Version](https://www.apple.com/shop/product/mw2h3am/a/35w-dual-usb-c-port-compact-power-adapter)
[70 Watts Version](https://www.apple.com/shop/product/mxn53am/a/70W%20USB-C%20Power%20Adapter)
[140 Watts Version](https://www.apple.com/shop/product/mw2m3am/a/140w-usb-c-power-adapter)

The PSU included with the FydeTab Duo is good too; however, it cannot be purchased separately.

</details>

## 3.2 如何确定我积木的功率输出？

虽然大多数充电器和供电器都为其最大功率输出作广告，但对于它们所支持的所有电压来说却不是这样。 如果我们检查Orange Pi PD100W，它的规格就会在它们的产品页面和电源砖本身上列出。 要确定手表中的电源输出, 你需要用安培乘坐电压。

<br>

$Voltage \* Ampere = Watt$

<div style="display:flex; align-items:flex-start; gap:20px;">

<div style="flex:1;">

<br>

| 电压       | Ampere    | 瓦特     |
| -------- | --------- | ------ |
| 5 Volts  | 3 Amperes | 15 瓦特  |
| 9 Volts  | 3 Amperes | 27 瓦特  |
| 12 Volts | 3 Amperes | 36 瓦特  |
| 15 Volts | 3 Amperes | 45 瓦特  |
| 20 Volts | 5 Amperes | 100 瓦特 |

从这个列表中，我们可以确定这个砖块能够为橙色Pi 6 Plus提供动力， 因为它要求从积木中获得20V，最多提供100瓦供使用。 它的前身Orange Pi 5 Plus从砖块中请求5V，并且只获得这种电力供应的15W。 这笔钱几乎不足以使这个SBC获得电力，因为它的芯片(RK3588)可以自己拿15W。 此外，Orange Pi 5 Plus的产品页将其电力要求定为5V/4A或20W。

</div>

<img src="/psu-charger/100wpsu.png" style="max-width:350px;">

</div>

## 3.3 USB-C输送电力是什么，为什么它很重要？

如上表所示，遵守USB-C PD标准的充电器和PSU可以提供多个输出电流。 如果您的电源砖，SBC和电缆(更多电缆)都支持PD, 您的设备能够通过USB-C电缆进行通信，以确定电砖和SBC的可接受电压和安培。 这种沟通使他们能够选择最好的组合。 并非所有设备都正确支持或实现此功能。 例如，Orange Pi 5 Plus不支持USB-C PD，尽管使用USB-C端口为棋盘供电。 相比之下，Radxa Rock 5/5B在9V/2A、12V/2A、15V/2A和20V/2A支持USB-C PD。

由于USB-C电源配送是USB-C特性的一部分，它不被USB-A支持。 如果没有 USB-C PD 通信，你的电源积木的输出电压将为 5 伏。

> USB-C PD 通信应总是在5伏特发生，但有些电源积木不正确地实现了这一功能。 这些电源积木可能会在最后一个已知的电流中尝试PD通讯，从而潜在地破坏你的SBC。 这种积木很少，但确实存在。
> {.is-info}

## 3.4 What about multi-port chargers?

Some USB power supplies come with multiple ports, either USB-A or USB-C. As USB-A can only output 5 volts and therefore don't do USB-C PD, those ports are not problematic. However, if your PSU has multiple USB-C ports, the charger must handle USB-C PD for any connected device.

Most PSUs implement this feature simply: they initiate the USB-C PD process whenever a new device is connected to any port. Therefore, if you're powering your SBC with one port and then connect another device, it will reset power to establish USB-C PD, which in turn resets your SBC as well. Thus, if you plan on using a multi-port brick, avoid connecting new devices while it powers your SBC.

# 5. 电缆；它们也不是所有的

正如你们可能已经猜到的那样，如果所有电缆都是一样的，本章将不存在。 USB电缆在两个插件之间的铜线线路上有所不同，但不是插件本身。 下表显示了不同铜线路支持的USB标准。

\| USB standard | VCC & GND | Data Plus / Minus | SSTX+ / SSTX− & SSRX+ / SSRX− | CC1 / CC2 | SBU1 / SBU2 | TX1+ / TX1− & RX1+ / RX1− | TX2+ / TX2− & RX2+ / RX2− | GND_DRAIN / Shield | Supported Power |
\| ------- | ------- | ------ | ------- | ------- | ------ | ------- | ------- | ------ |
\| USB 1.1 & 2.0 | X | X | | | | | | | 2.5 Watts |
\| USB 3.x | X | X | X | | | | | X | 15 Watts |
\| USB-C minimal | X | X | | X | X | | | | 60 Watts |
\| USB-C full | X | X | | X | X | X | | X | 240 Watts |
\| USB-C Thunderbolt | X | X | | X | X | X | X | X | 240 Watts |

虽然该表区分了三类美国广播公司电缆，但最终取决于制造商在电缆中使用多少铜。 由于铜是昂贵的，正如你们可能猜到的那样，许多制造商降低了这些电缆的成本。 此外，仅仅因为USB电缆在两端都有USB-C插件，不意味着它支持任何 USB-C标准。 您可以简单地使用 USB -C插件制造一个 USB 2.0兼容的电缆，然后低价出售它们。 这些类型的电缆通常在加油站、机场或杂货店销售。 它们通常在包装上没有任何评级，通常只提供2.5瓦，类似于“普通”USB 2.0 电缆。

> 不要购买这种电缆！ 他们很慢，很有可能抓到火力！
> {.is-info}

需要考虑的另一个方面是存在着所谓的“电子标记”芯片。 此chips 拥有关于您有线电视的功能的信息。 没有这个芯片，电缆可以最大输送60瓦。 通过30个特设工作组铜的连接，运送60瓦可能具有潜在的危险；但是，电源砖和BBC都不会发现这个问题。 如有必要，委员会可继续绘制60瓦，直到电缆发生火灾。 大多数国家都禁止有抓获火力的电缆，但这并不阻止任何人出售电缆。

## 4.1 Does cable length matter?

In an ideal world, a USB-C cable should function perfectly up to a length of 3 meters; however, as demonstrated in the previous article, we don't live in such a perfect world.

Longer cables encounter two primary issues. First, any cable can act as an antenna if not properly shielded, ironically the shielding itself acts like an antenna by redirecting captured signals to ground, so those signals can not affect any internal wires. The longer the cable, the more effectively it functions as an antenna, making good shielding essential for both internal wire pairs and the entire cable.

The second issue arises from the internal resistance of the copper connections. As previously discussed, manufacturers often reduce costs by omitting some copper connections. Another cost-saving measure is thinning these connections, which increases their internal resistance. This presents two problems: First, continuously drawing high power through thin cables generates heat. If this heat cannot dissipate—for example, if your cable is concealed in a duct—it could eventually lead to fire. The second, more common issue is that increased resistance affects voltage levels. Assuming a cheap cable has a resistance of 0.25 Ω and our SBC operates on 5V/2A, the calculation goes as follows:

$2 A × 0.25 Ω = 0.5 V$

This results in a voltage drop of 0.5 volts. Thus, while the power brick outputs 5 volts, only 4.5 volts reach your SBC.

The rule of thumb is that the longer your cable, the better its construction must be. It's best to use the shortest cable possible for your setup, but don't exceed 1.5 meters of cable length.

If you really need to exceed 1.5 meters we recommend the use of an [Apple USB-C Cable](https://www.apple.com/shop/product/myqt3am/a/240w-usb-c-charge-cable-2-m).

## 4.2 How to determine which kind of cable i have?

除了USB-A电缆之外，如果它们支持 USB 3 和任何其他的 USB 1颜色，它们有蓝色插拔。 或 2.0，只有两种方法来确定如何构建它们。

最简单但又具有破坏性的方法是把车厢的护盾绑起来，并计算两端之间的铜联系。 如果仔细操作，电缆可能在以后仍然可以使用；然而，由于USB-C是为高速和高频应用设计的，这种操作无法保证。

另一种方法是使用电缆测试器。 在像AliExpress这样的平台上可以找到这些成本低廉的东西。 典型的情况是，你将电缆两端插入测试器。 其LED灯能点燃以显示电缆中存在的任何铜连接。

这两种方法都不能在店内或在网上购买。 作为缩略图的规则，请检查软件包或产品页面的评分。 此外，当在当地商店购买电缆时，你可以通过感受它们的强度来测量它们的质量。 一般而言，更加严格的情况表明电缆内有更好的防护和更多的铜连接。 至少避免购买现有最便宜的电缆或您将感到失望。

> The Youtube channel "GreatScott!" has made a great two part series about USB-C cables found [here (Part one)](https://www.youtube.com/watch?v=ZikvlsVDiQY) and [here (Part two)](https://www.youtube.com/watch?v=LOIVrVVYBfA).
> {.is-info}

# 4. 如何处理所有这些信息？

在阅读了所有这些之后，你可能会得出这样的结论，即这种情况相当复杂。 你是正确的！ 如果您遇到了“2”部分描述的问题。 什么时候我需要考虑这个？"，请检查您的SBC、电源积木和电缆的产品页面。 如果您找不到任何关于评分的信息，请停止使用那个电源积木或电缆。

如果您在购买PSU之前阅读了这篇文章, 请考虑如何使用您的看板。 例如，如果你想要使用一个 Orange Pi 5 Plus, 带有两个旋转硬盘, 各为 5V/1A 级, 只需添加这些值:

20W+5W+5W=30W$

然后确保你的电砖不会负担过重， 计算它应提供多少功率以使其正常使用约80%：

30 W / 0.8 =37.5W$

在这种情况下，我们建议至少给予37.5瓦的PSU等级。