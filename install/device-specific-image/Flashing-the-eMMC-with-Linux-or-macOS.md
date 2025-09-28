---
title: Flashing the eMMC with Linux or macOS
description: 
published: true
date: 2025-09-28T12:16:17.455Z
tags: 
editor: markdown
dateCreated: 2025-09-16T06:29:26.865Z
---

# 1. Introduction
This guide describes how to flash an eMMC using the tool `rkdeveloptool`. It can be found in most Linux repositories and also runs on macOS.

For the installation of BredOS, three things are required:
1. SPL loader file, for example for the RK3588:  [`rk3588_spl_loader_v1.15.113.bin`](https://dl.radxa.com/rock5/sw/images/loader/rk3588_spl_loader_v1.15.113.bin)
2. Device Specific Image from our [official website](https://bredos.org/download.html)
3. `rkdeveloptool`

> Other Rockchip chip variants require different SPL loaders!
\
For example, for the RK3566, the SPL loader can be found here:
[`rk356x_spl_loader_ddr1056_v1.10.111.bin`](https://dl.radxa.com/rock3/images/loader/rock-3a/rk356x_spl_loader_ddr1056_v1.10.111.bin)
{.is-warning}


# 2. Installation
The installation of `rkdeveloptool` can be done with the following steps.

## 2.1 Linux
- If you are using an Arch-based distribution
```
sudo pacman -S rkdeveloptool-git
```
- If you are using an Debian-based distribution
```
sudo apt install rkdeveloptool
```
- If you are using an Red Hat-based distribution
```
sudo dnf install rkdeveloptool
```

## 2.2 macOS
### 2.2.1 Prerequisites
As there is no binary package for `rkdeveloptool` for macOS, we need to compile it ourselves. To do that, we need to have some packages installed via [Brew](https://brew.sh/). 
- Install `automake`, `autoconf`, `libusb`, `pkg-config`, `git` and `wget` with the following command:
```
brew install automake autoconf libusb pkg-config git wget
```
### 2.2.2 Clone Repository
- Get the source code with:
```
git clone https://github.com/rockchip-linux/rkdeveloptool
```
### 2.2.3 Compile to binary
- Now change into the directory that contains the source code and complie it:
```
cd rkdeveloptool
autoreconf -i
./configure
make -j $(nproc)
```

- After the process `make` has finished without an error there is the file `rkdeveloptool` inside your current folder:
```
ls | grep rkdeveloptool
```
- That should output:
```
rkdeveloptool
```

### 2.2.4 Make it executable
- And finally copy it to the `opt` folder to run it from everywhere:
```
cp rkdeveloptool /opt/homebrew/bin/
```

# 3. Flashing
## 3.1 Enter maskrom
For the SBC to show up as a flashable device over USB, it needs to be set to `maskrom mode`. This can be achieved differently depending on the device you are using. Some SBCs have a button, while others require you to short two pins. Please refer to the documentation of your SBC manufacturer.

- This information can easily be found with a Google search:
```
maskrom mode <your sbcs name here>
```

- To verify that your device is in `maskrom mode` and has correctly discovered by your PC run:
```
sudo rkdeveloptool ld
```

- If you see the following, you are good to go (output is similar, but not identical):
```
DevNo=1 Vid=0x2207,Pid=0x350b,LocationID=801 Maskrom
```

> The Maskrom button should be held down **while power is being plugged** into the board.
{.is-info}

> Using USB-C to C cables, or a USB-C to A cable backwards may result to the board not being detected.
It is recommended to use a USB-C to A cable, then a [USB-C Female to USB-A Male adapter](https://www.aliexpress.com/item/1005004767752226.html) or a USB-A to A cable.
{.is-warning}

## 3.2 Flash BredOS
Now that we are able to send commands to the device with `rkdeveloptool`, lets make a BredOS SBC out of it. 

- Send the SPI loader file to your SBC:
```
sudo rkdeveloptool db <path to SPI loader file here>
```

- Then write the BredOS Device Specific Image to its eMMC:
```
sudo rkdeveloptool wl 0 <path to BredOS image here>
```

- And finally reboot your device:
```
sudo rkdeveloptool rd
```

> After successful flashing proceed with [**First Setup**](/en/install/first-setup).
{.is-success}