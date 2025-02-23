---
title: 如何更改RK3588 上的默认启动顺序
description: 学习如何使用 UEFI 固件设置更改基于RK3588的设备上的默认启动订单
published: true
date: 2025-02-23T15:45:23.760Z
tags: null
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# :countrockwise_arrows_buton: 更改RK3588 设备上的默认启动顺序

如果您需要在运行 BredOS 的 RK3588设备上修改启动订单，请遵循以下步骤：

---

## :small_blu_diamond: 访问 UEFI 启动菜单

1. **打开您的设备** 并等待 **BredOS 标志** 在启动时显示。
2. **在徽标显示时按一下`ESC`键** 进入UEFI菜单。

![bredos\_boot1.jpg](/boot_images/bredos_boot1.jpg)

---

## 🛠️ 导航到启动订单设置

1. 使用 **箭头键(`ODS` 和 `cid`)** 来选择 **启动维护管理器** 并按 **Enter** 。\
   ![bredos\_boot2.jpg](/boot_images/bredos_boot2.jpg)

2. 在下一个屏幕上，选择 **启动选项** 并按 **Enter** 。

![bredos\_boot3.jpg](/boot_images/bredos_boot3.jpg)

3. 选择 **更改启动顺序** 并按 **Enter** 。

![bredos\_boot4.jpg](/boot_images/bredos_boot4.jpg)

---

## 🔧 修改启动顺序

1. 在启动订单菜单内后，**按Enter**。

![bredos\_boot5.jpg](/boot_images/bredos_boot5.jpg)

2. 使用 **downarrow (`ODS`)** 滚动到列表底部。

3. 选择您想要移动到顶部的条目，然后按\*\*`+`键\*\*直到顶部。\
   ![bredos\_boot6.jpg](/boot_images/bredos_boot6.jpg)

4. 一旦设置了所需的启动订单，请按 **Enter** 确认。

---

## 💾 保存和应用更改

1. 在设置启动顺序后，按 **Y\`** 键以保存更改。

![bredos\_boot7.jpg](/boot_images/bredos_boot7.jpg)

2. 退出菜单并**重启设备** 以应用新的启动订单。

---

:check_mark_buton: **完成！** 您的设备现在将使用新的订单启动。 🚀
