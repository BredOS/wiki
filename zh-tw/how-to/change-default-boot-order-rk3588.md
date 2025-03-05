---
title: How to Change the Default Boot Order on RK3588
description: Learn how to change the default boot order on RK3588-based devices using the UEFI firmware settings
published: true
date: 2025-02-23T15:45:23.760Z
tags: null
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 🔄 Changing the Default Boot Order on RK3588 Devices

If you need to modify the boot order on an RK3588-based device running BredOS, follow these steps:

---

## 🔹 Accessing the UEFI Boot Menu

1. **Turn on your device** and wait for the **BredOS logo** to appear during boot.
2. **Press the `ESC` key once** while the logo is displayed to enter the UEFI menu.

![bredos_boot1.jpg](/boot_images/bredos_boot1.jpg)

---

## 🛠 Navigating to the Boot Order Settings

1. Use the **arrow keys (`↓` and `↑`)** to select **Boot Maintenance Manager** and press **Enter**.\
  ![bredos_boot2.jpg](/boot_images/bredos_boot2.jpg)

2. On the next screen, select **Boot Options** and press **Enter**.

![bredos_boot3.jpg](/boot_images/bredos_boot3.jpg)

3. Choose **Change Boot Order** and press **Enter**.

![bredos_boot4.jpg](/boot_images/bredos_boot4.jpg)

---

## 🔧 Modifying the Boot Order

1. Once inside the boot order menu, **press Enter**.

![bredos_boot5.jpg](/boot_images/bredos_boot5.jpg)

2. Use the **down arrow (`↓`)** to scroll to the bottom of the list.

3. Select the entry you want to move to the top and press the **`+` key** until it reaches the top.\
  ![bredos_boot6.jpg](/boot_images/bredos_boot6.jpg)

4. Once the desired boot order is set, press **Enter** to confirm.

---

## 💾 Saving and Applying the Changes

1. After setting the boot order, press **`Y`** to save the changes.

![bredos_boot7.jpg](/boot_images/bredos_boot7.jpg)

2. Exit the menu and **restart the device** to apply the new boot order.

---

✅ **Done!** Your device will now boot using the new order. 🚀
