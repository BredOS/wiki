---
title: 更改RK3588 上的启动订单
description: 学习如何使用 UEFI 固件设置更改基于RK3588的设备上的默认启动订单
published: true
date: 2025-09-16T10:42:14.944Z
tags:
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 1. 简介

如果您需要在运行 BredOS 的 RK3588设备上修改启动订单，请遵循以下步骤：

# 2. 访问 UEFI

## 2.1 访问启动菜单

- 打开您的设备并等待 BredOS 标志在启动时出现。
- 在徽标显示时按一下`ESC`键进入UEFI菜单。

![bredos_boot1.jpg](/boot_images/bredos_boot1.jpg)

## 2.2 导航到启动订单设置

- 使用箭头键(`ODS` 和 `did `) 选择`启动维护管理器` 并按 `Enter`。

![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

- 在下一个屏幕上，选择 `Boot Options` 并按 `Enter` 键。

![bredos_boot3.jpg](/boot_images/bredos_boot3.jpg)

- 选择 `Change Boot Order` 并按 `Enter` 键。

![bredos_boot4.jpg](/boot_images/bredos_boot4.jpg)

## 2.3 修改启动订单

- 在启动订单菜单中，请按 `Enter`。

![bredos_boot5.jpg](/boot_images/bredos_boot5.jpg)

- 使用下箭头(“ODS”) 滚动到列表底部。
- 选择您想要移动到顶部的条目，然后按下 "+" 键到达顶部。

![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

- 一旦设置了所需的启动订单，请按 `Enter` 键确认。

## 2.4 保存和应用更改

- 设置启动顺序后，按`Y`保存更改。

![bredos_boot7.jpg](/boot_images/bredos_boot7.jpg)

- 退出菜单并重启设备以应用新的引导顺序。

> 完成！ 您的设备现在将使用新的订单启动。
> {.is-success}

