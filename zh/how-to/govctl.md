---
title: 配置省长
description: 使用 govctl 管理系统管理器
published: true
date: 2025-05-07T12:47:49.033Z
tags:
editor: markdown
dateCreated: 2025-05-07T12:47:49.033Z
---

# 使用 GovCtl

默认情况下，BredOS船在包`bredos-govctl`中的工具`govctl` 。
它默认启用，并将根据可用电池电量设定性能。

工具将持续将调节器设置为指定的设置，覆盖或其他工具将不起作用。
如果您的工作流出现问题，请卸载软件包。

## 默认行为

GovCtl 默认将确保所有附加设备的最大性能，如果没有机载电池，或者系统已插入。

如果系统有足够的收费，但没有接入，它将保持大部分性能，限制GPU速度和cpu推力。

如果系统没有足够的电荷（20%是确定电荷的默认点），
该系统将尽量减少电力，从而损害性能和响应时间。
例如，这将使RK3588板只能运行在300毫赫中。

如果你不喜欢默认，它们都可以更改。

# 查看调节器状态

要查看当前应用的管理器，只需运行 `govctl`，根权限是不需要的。

```
[bill88t@icu | ~]> govctl

---------------------------------------
Currently applied governor: performance
---------------------------------------

usage: govctl [-h] [-g {powersave,conservative,performance}]
              [-b {powersave,conservative,performance}] [-e] [-d]
              [-p POWERSAVE_PERCENT]

Governor configuration tool

options:
  -h, --help            show this help message and exit
  -g, --set-governor {powersave,conservative,performance}
                        Set desired governor
  -b, --set-battery-governor {powersave,conservative,performance}
                        Set desired governor while running on battery power
  -e, --enable-battery-detection
                        Enable battery state detection
  -d, --disable-battery-detection
                        Disable battery state detection
  -p, --powersave-percent POWERSAVE_PERCENT
                        Percentage at which powersave triggers
```

# 设置不同的节能点

如帮助菜单所述，使用选项 `-p` 将允许您重新配置`powersave` 应用的点。 默认为20%，可设定为1%到80%。

重新编排如下：

```
sudo govctl -p 30
```

这将使其触发力达到30%。

# 更改应用的调速器

默认情况下，当插入电池或没有电池时，系统将保持最大性能。
如果您想应用更加保守的电源配置文件，请运行：

```
sudo govctl -g 保守的
```

如果您想要保持最大性能，即使未接入，请运行：

```
sudo govctl -b 业绩
```

标志`-g`设置插电时使用的调速器。
Glag `-b`设置了当\*\*未插入时使用的调速器。

# 禁用电池检测

禁用电池检测方式：

```
sudo govctl -d
```

将确保在任何时候都应用“已接入”调速器。

要撤消此操作，请运行：

```
sudo govctl -e
```