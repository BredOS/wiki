---
title: 如何更改RK3588 上的默认启动顺序
description: 学习如何使用 UEFI 固件设置更改基于RK3588的设备上的默认启动订单
published: true
date: 2026-01-08T17：55：29.490Z
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

<details>
<summary><b>屏幕截图</b></summary>

![uefi-boot-screen.png](/boot_images/uefi-boot-screen.png)

</details>

## 2.2 导航到启动订单设置

- 使用箭头键(`ODS` 和 `did `) 选择`启动维护管理器` 并按 `Enter`。\
  ![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

<details>
<summary><b>屏幕截图</b></summary>

![options-main.png](/boot_images/options-main.png)

</details>

- 在下一个屏幕上，选择 `Boot Options` 并按 `Enter` 键。

<details>
<summary><b>屏幕截图</b></summary>

![optione-boot-maint-manager.png](/boot_images/optione-boot-maint-manager.png)

</details>

- 选择 `Change Boot Order` 并按 `Enter` 键。

<details>
<summary><b>屏幕截图</b></summary>

![options-change-boot-order.png](/boot_images/options-change-boot-order.png)

</details>

## 2.3 修改启动订单

- 在启动订单菜单中，请按 `Enter`。

<details>
<summary><b>屏幕截图</b></summary>

![show-boot-order.png](/boot_images/show-boot-order.png)

</details>

<details>
<summary><b>屏幕截图</b></summary>

![change-boot-order.png](/boot_images/change-boot-order.png)

</details>

- 使用下箭头(“ODS”) 滚动到列表底部。
- 选择您想要移动到顶部的条目，然后按下 "+" 键到达顶部。\
  ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

<details>
<summary><b>屏幕截图</b></summary>

![change-boot-order-finished.png](/boot_images/change-boot-order-finished.png)

</details>

- 一旦设置了所需的启动订单，请按 `Enter` 键确认。

## 2.4 保存和应用更改

- 设置启动顺序后，按`Y`保存更改。

<details>
<summary><b>屏幕截图</b></summary>

![change-boot-order-save.png](/boot_images/change-boot-order-save.png)

</details>
- Exit the menu and restart the device to apply the new boot order.  

> 完成！ 完成！ 完成！ 您的设备现在将使用新的订单启动。
> {.is-success}
> {.is-success}
> {.is-success}

