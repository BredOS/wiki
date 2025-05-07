---
title: DTSC Helper Script
description: Using the BredOS Device Tree Source Compiler helper script
published: true
date: 2025-05-07T13:40:24.351Z
tags: 
editor: markdown
dateCreated: 2025-05-07T13:18:58.736Z
---

# DTSC Helper Script

`dtsc` is a command shipped by default along with BredOS along with the `bredos-tools` package.
For it to function however you need to install `dtc`, simply run `yay -S dtc`

The script is a wrapper to dtsc, performing automatic gcc preprocessing, linking and generation of needed files.
It makes generation and testing of device trees a lot simplier.
It automatically determines and generates base device trees or overlays accordingly.

## IMPORTANT NOTE

**Installing an incorrect device tree on your device will render it inoperable.**
**Be careful, perform backups and ensure a contigency plan.**

# Usage

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

## Input

The script expects an input `.dts` file. If no output is specified, it generated a matching-name `.dtb`
The output filename can be set with the `-o` parameter.

## Linking against kernel

If you have more than one kernels installed onto your system, you should specify the kernel path to link against.
It should look something like this:
```
dtsc example.dtc -k /usr/src/linux-rockchip-rkr3 -o example.dtbo
```

If you have a single kernel installed, this will automatically be detected.

## Compiling base Device Trees

If you're compiling a base device tree and not an overlay, you'll need your kernel's full sources, which are not shipped.
This is because these trees require the inclusion of other `.dtsi` device trees.

To compile such a DT, clone your kernel's repository using git, onto a known path.

Example for the `linux-rockchip-rkr3` kernel:
```
git clone https://github.com/BredOS/linux-bredos
```

Then run dtsc as you would, but with the `-i` flag, specifying the folder at which the files it wants to link against are.

For example, assuming we want to compile a rk3588 board's DT, we'll need to specify the options as follows:
```
dtsc rk3588-example-board.dts -i /path/to/linux-bredos/arch/arm64/boot/dts/rockchip -o rk3588-example-board.dtb
```