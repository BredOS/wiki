---
title: Mainline campaign
description: 
published: false
date: 2025-09-22T18:19:42.854Z
tags: 
editor: markdown
dateCreated: 2025-09-22T17:56:04.573Z
---

## Milestone Campaign: Mainline RK3588 Support in BredOS

Right now, BredOS images for RK3588 devices rely on the crusty Rockchip BSP kernel — a huge, duct-taped codebase that’s hard to maintain, insecure, and always lags behind upstream Linux.

We want to change that.

By mainlining RK3588 support, BredOS will bring:

- Long-term maintainability (no more chasing BSP hacks)

- Upstream kernel security fixes

- Better performance and stability

- Support across all RK3588 devices (SBCs, dev boards, mini-PCs)

- A solid foundation for ARM64 desktop and server use

This is about making BredOS — and the wider Linux ecosystem — better for everyone using RK3588 hardware.

## Why Are We Doing This?
A fair question we often hear is: *“Isn’t RK3588 already mainlined?”*  
The truth is: **only part of it is**.  

While much of the low-level backend work (like basic kernel support) has landed upstream, **day-to-day essentials are still broken or missing**:  
- Many Wi-Fi drivers don’t work out of the box  
- Device-specific optimizations aren’t covered by generic mainline patches  

In BredOS, we want RK3588 devices to be **practical and polished for real users**. That means:  
- Reliable Wi-Fi and networking  
- Optimized fan profiles (quiet when idle, cooling under load)  
- Stable GPU and multimedia support  
- Proper installer and images ready to flash  

This campaign isn’t just about “making it boot.” It’s about making RK3588 devices **actually usable**.

## Benefits of Mainline
Thanks to our early mainline experiments, we’ve already seen some exciting advantages:  
- **2× Vulkan performance** over BSP builds and more GPU goodies
- **Proper VPU implementation** that doesn’t require the custom Rockchip Media Processing Platform (MPP)
- Ability to run **Chromium or any video-accelerated apps** out-of-the-box  
- No more custom hacks or recompiles for common video workloads  

Mainline unlocks these **real, tangible improvements** for both developers and end-users, making RK3588 devices far more capable in daily use.



## How You Can Help
- **Donate**: Every contribution brings us closer to a mainlined RK3588 experience. You can contribute [here](https://ko-fi.com/Z8Z3I4J0P) or PM @rippanda12
- **Share**: Spread the word in RK3588 communities, SBC forums, and social media.  
- **Sponsor**: Companies depending on RK3588 hardware can back this milestone at higher tiers (we’ll credit sponsors in our repo and website).  


##  What We’ll aim to do
1. **Upstreaming & Kernel Work**
   - Rebase patches onto mainline kernel  

2. **Boot & Install Support**
   - Support for standard ARM64 boot flow (UEFI where possible)  
   - Build proper BredOS mainline images for RK3588 boards  

3. **Testing & CI**
   - Automated test builds for popular boards (e.g., Orange Pi 5, Rock 5B)  
   - Continuous integration with mainline updates  

4. **User Experience**
   - Ensure GPU, networking, storage, and I/O are stable  
   - Provide prebuilt, ready-to-flash images for end users 
   

## Where the Money Goes
- Developer time (kernel, bootloader, userspace integration)
- CI infrastructure for ongoing builds and testing  



**[Support the RK3588 Mainline Milestone Now](https://ko-fi.com/Z8Z3I4J0P)**
