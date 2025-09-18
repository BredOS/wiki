---
title: BredOS Tools
description: Utilities and Tools provided by BredOS
published: true
date: 2025-09-16T10:29:53.626Z
tags:
editor: markdown
dateCreated: 2025-05-07T18:27:16.781Z
---

# 1. 簡介

This is shipped as `bredos-tools`, compatible with any system architecture, on the `BredOS-any` repository.
It is an integral part of BredOS. `bredos-tools` should be installed by default.

- If not install it with:

```
sudo pacman -S bredos-tools
```

This package contains a plethora of tools with the sole purpose of easing development, maintenance and the general use of BredOS.

# 2. GRUB Password Protection

BredOS includes a utility to restrict GRUB boot options with a password.
This prevents unauthorized users from booting non-default entries or editing boot parameters.

## 2.1 Enable GRUB Password

- To enable grub password protection, execute:

```
sudo grub-password
```

You’ll be prompted to enter and confirm a password.
Once set, only the default GRUB entry can be booted without authentication.

## 2.2 Disable GRUB Password

- To disable grub password protection, execute:

```
sudo grub-password -d
```

This removes the password restriction and restores normal GRUB behavior.

> The configuration is stored in /etc/grub.d/99-bredos-grub-password.
> The script regenerates GRUB config automatically via grub-mkconfig.
> This modifies `/etc/grub.d/10_linux`, do not revert it manually!
> {.is-info}

# 3. DTSC Helper Script

- For it to function you need to install `dtc`, simply run

```
yay -S dtc
```

The script is a wrapper to dtc, performing automatic gcc preprocessing, linking and generation of needed files.
It makes generation and testing of device trees a lot simplier.
It also automatically determines and generates base device trees or overlays accordingly.

> Installing an incorrect device tree on your device will render it inoperable.
> Be careful, perform backups and ensure a contigency plan.
> {.is-warning}

## 3.1 Usage

- Run dtsc with the parameter `-h` to show its usage:

```
usage: dtsc [-h] [-o OUTPUT] [-i INCLUDE] [-k KERNEL] [input]

Compile a Device Tree Source (DTS) file into a Device Tree Blob (DTBO or DTB).

positional arguments:
  input                 Input DTS file

options:
  -h, --help            show this help message and exit
  -o, --output OUTPUT   Output file (default: makes input_filename.dtb)
  -i, --include INCLUDE
                        Source of additional device tree files (optional)
  -k, --kernel KERNEL   Manualy specify a kernel source path (default:
                        autodetect)

Example: ./compile_dts.py my_device_tree.dts -o output.dtbo
```

## 3.2 Input

The script expects an input `.dts` file. If no output is specified, it generated a matching-name `.dtb`
The output filename can be set with the `-o` parameter.

## 3.3 Linking against kernel

If you have more than one kernels installed onto your system, you should specify the kernel path to link against.

- It should look something like this:

```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

If you have a single kernel installed, this will automatically be detected.

## 3.4 Compiling base Device Trees

If you're compiling a base device tree and not an overlay, you'll need your kernel's full sources, which are not shipped.
This is because these trees require the inclusion of other `.dtsi` device trees.

To compile such a DT, clone your kernel's repository using git, onto a known path.

- Example for the `linux-rockchip-rkr3` kernel:

```
git clone https://github.com/BredOS/linux-bredos
```

Then run dtsc as you would, but with the `-i` flag, specifying the folder at which the files it wants to link against are.

- For example, assuming we want to compile a rk3588 board's DT, we'll need to specify the options as follows:

```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```