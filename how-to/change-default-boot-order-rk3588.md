---
title: Change the Boot Order on RK3588
description: Learn how to change the default boot order on RK3588-based devices using the UEFI firmware settings
published: true
date: 2026-01-08T17:55:29.490Z
tags: 
editor: markdown
dateCreated: 2025-02-23T15:45:23.760Z
---

# 1. Introduction

If you need to modify the boot order on an RK3588-based device running BredOS, follow these steps:

# 2. Accessing the UEFI
## 2.1 Accessing the Boot Menu

- Turn on your device and wait for the BredOS logo to appear during boot.  
- Press the `ESC` key once while the logo is displayed to enter the UEFI menu.  


<details>
<summary><b>Screenshot</b></summary>

  ![uefi-boot-screen.png](/boot_images/uefi-boot-screen.png)
  
</details>

## 2.2 Navigating to the Boot Order Settings

- Use the arrow keys (`↓` and `↑`) to select `Boot Maintenance Manager` and press `Enter`.  


<details>
<summary><b>Screenshot</b></summary>

  ![options-main.png](/boot_images/options-main.png)
  
</details>


- On the next screen, select `Boot Options` and press `Enter`.  

<details>
<summary><b>Screenshot</b></summary>

  ![optione-boot-maint-manager.png](/boot_images/optione-boot-maint-manager.png)
  
</details>

- Choose `Change Boot Order` and press `Enter`.  


<details>
<summary><b>Screenshot</b></summary>

  ![options-change-boot-order.png](/boot_images/options-change-boot-order.png)
  
</details>


## 2.3 Modifying the Boot Order  

- Once inside the boot order menu, press `Enter`.  

<details>
<summary><b>Screenshot</b></summary>

  ![show-boot-order.png](/boot_images/show-boot-order.png)
  
</details>

<details>
<summary><b>Screenshot</b></summary>

  ![change-boot-order.png](/boot_images/change-boot-order.png)
  
</details>

- Use the down arrow (`↓`) to scroll to the bottom of the list.  
- Select the entry you want to move to the top and press the `+` key until it reaches the top.  


<details>
<summary><b>Screenshot</b></summary>

  ![change-boot-order-finished.png](/boot_images/change-boot-order-finished.png)
  
</details>


- Once the desired boot order is set, press `Enter` to confirm.  

## 2.4 Saving and Applying the Changes

- After setting the boot order, press `Y` to save the changes.  


<details>
<summary><b>Screenshot</b></summary>
	
  ![change-boot-order-save.png](/boot_images/change-boot-order-save.png)
  
</details>
- Exit the menu and restart the device to apply the new boot order.  

> Done! Your device will now boot using the new order.
{.is-success}

