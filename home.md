---
title: Homepage
description: 
published: true
date: 2025-10-06T05:41:19.201Z
tags: 
editor: markdown
dateCreated: 2022-08-24T12:37:36.410Z
---

# 1. Overview
Welcome to the BredOS documentation! BredOS is a user-friendly Arch-based Linux distribution specifically designed for ARM and RISC-V based single board computers (SBCs).
The documentation will guide you through the installation, configuration, and usage of BredOS.

![boot-no-loop.gif](/boot-no-loop.gif)

# 2. Features
 - We ship functional installations, not configurations.
 - No experience required. It’s easy; everything is documented, and [we love to help](#h-8-community-and-support)!
 - Simple and plain by design! No bloat, ensuring a lightweight and responsive system!
 - Arch-based - with customization tailored to be polished and easy to use.

## 2.1 Featured tools

 - Bakery - [your guide to your own Bred](/install/first-setup)!
 - Bred-News - [the news channel about your Bred](/en/customizations/news)!
 - Bred-Tools - [the swiss knife at your hand](/Tools)!
 - Bred-Config - [like raspi-config, but with better taste!](/bredos-config)
 - Govctl - [take control of your CPU](/how-to/govctl)!
 
 # 3. System Requirements
We support a wide range of devices—from exciting ARM-based systems and experimental RISC-V setups to plain old lame x86_64 intel/amd boards. We've got you covered, whether you use our [mainline .iso installation](/install/Installation-with-ISO) or refer to the list of devices we passionately support on our [table of supported devices](/table-of-supported-devices).
 
## 3.1 Minimal System Requirements
 - Minimum RAM: 2 GB
 - Storage: 8 GB microSD card/eMMC/NVMe or larger
 
# 4. Preview
Our friend [**DroidMaster**](https://www.youtube.com/@LinuxDroidMaster) made a YouTube video about BredOS. Check it out here:
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/eoLE27xdtu4?si=ai-0QqLNyCYfTKfA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
 
# 5. Download
You can find download links for images in our [website](https://bredos.org/download.html)!

# 6. Installation
To make installation easy for you, we laid out a line of bred crumbs for you to follow.

## 6.1 Device specific image installation
These are images for the boards we love the most. To install these BredOS images on them, either start with our [device specific image](/install/device-specific-image) installation guide, or take a glimpse to the device page at our wiki, which can be found in the navigation bar left of this.

Visit our [download site](https://bredos.org/download.html) to find out if your device is one of them.

## 6.2 Generic installation
If your device isn’t listed on our [download site](https://bredos.org/download.html) but supports booting UEFI and is based on either x86_64- or ARM64 architecture, simply follow our guide for a generic installation available [here](/install/Installation-with-ISO).

## 6.3 Docker container installation
- Easy as one line of command:
```
docker pull bredos/bredos
```

# 7. Troubleshooting
Take a look at the device pages in the navigation bar on this page to find known issues specific to your device. If your problem is not listed there, feel free to contact us directly via [our support channels](#h-8-community-and-support).

# 8. Community and Support
Join the BredOS community to get support, share ideas, and contribute to the project:
- [Telegram](https://t.me/bredoslinux)
- [Discord](https://discord.gg/jwhxuyKXaa)
- [GitHub](http://github.com/BredOS)
{.links-list}
# 9. Contributing
BredOS is an open-source project, and contributions are welcome! You can contribute in the following ways:
- Report bugs and issues
- Submit patches and improvements
- Write and improve documentation
- Help other users in the community forums and chat

# 10. Mainline Campaign
Right now, BredOS images for RK3588 devices rely on the crusty Rockchip BSP kernel — a huge, duct-taped codebase that’s hard to maintain, insecure, and always lags behind upstream Linux.

[We want to change that](/campaigns/mainline-campaign).

