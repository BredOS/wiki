---
title: Kernel modding
description: 
published: true
date: 2025-11-17T08:17:37.109Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# 1. Introduction

This guide primarily focuses on RK3588 and the linux-rockchip-rkr3 kernel; however, the general process and many of the concepts should also apply to other kernels and devices. Whether you are developing custom firmware, contributing to upstream kernel support, or simply seeking to understand how the Linux kernel is built for hardware, this article aims to provide a clear and practical starting point.

> Check out the table of branches at the end of this article to find out which branch to use for your device.
{.is-info}


# 2. Obtaining the kernel or it's source code
## 2.1 BredOS kernel Repository

BredOS stores it's `linux-rockchip` kernel fork at [https://github.com/BredOS/linux-bredos](https://github.com/BredOS/linux-bredos).

The branch used for the rkr3 kernel is `rk6.1-rkr3`, the mainline variant is instead at `rk-mainline`. While rkr3 (aka Legacy (stable) aka BSP) is the kernel we ship with our "device specific images", mainline is the most up-to-date kernel which still has bugs and missing features.

> For more info have a look [here](/en/img-types).
{.is-info}


## 2.2 Building BredOS Kernel
Like any custom PKGBUILD for BredOS, the kernel PKGBUILD can also be found at [https://github.com/BredOS/sbc-pkgbuilds](https://github.com/BredOS/sbc-pkgbuilds). In this example we build the rkr3 kernel, but this guide applies to all linux-kernel PKGBUILDs found in our repository.
- Clone the repository with:
```
git clone https://github.com/BredOS/sbc-pkgbuilds
```

This creates a folder with the name `sbc-pkgbuilds` in your current directory, which holds any custom package from our repository, including the kernel PKGBUILD.

- Change directory to the kernel PKGBUILD with:
```
cd sbc-pkgbuilds
cd linux-rockchip-rkr3
```

- The contents of that folder should be as follows:
```
PKGBUILD
bredos-update-dtbs
config
dtb-update.hook
linux.preset
```

- To compile and package the kernel, run:
```
makepkg -si
```

> While the parameter `-s` automatically installs all necessary dependencies, the parameter `-i` installs the package after successful compiling.
{.is-info}


## 2.3 Building the kernel with patches
To build the kernel with patches we need to implement the patch into PKGBUILD. Follow the section [2.2 Building BredOS Kernel](/en/development/kernel#h-2-2-building-bredos-kernel) but dont run the command `makepkg -si` yet.

- This is the example code of a patch:
```
diff --git a/init/version-timestamp.c b/init/version-timestamp.c
index 1111111111..2222222222 100644
--- a/init/version-timestamp.c
+++ b/init/version-timestamp.c
@@ -29,8 +29,10 @@
 
 /* FIXED STRINGS! Don't touch! */
 const char linux_banner[] =
-       "Linux version " UTS_RELEASE " (" LINUX_COMPILE_BY "@"
-       LINUX_COMPILE_HOST ") (" LINUX_COMPILER ") " UTS_VERSION "\n";
+       "Linux version this-is-a-private-kernel-dont-touch ";
 
-- 
```
> This example patch set a fixed name instead of a generated one to your compiled kernel.
{.is-info}


Save your patch to a .patch file next to the file `PKGBUILD`. In this example we save the code above as `example.patch`.

- To implement the patch into PKGBUILD, run:
```
nano PKGBUILD
```

- Look up the `prepare` section. It should look like this:
```
prepare() {
  cd linux-bredos

  cp ${srcdir}/config .config
}
```

- And add your patch after `cd linux-bredos`:
```
prepare() {
  cd linux-bredos

  git apply ../../example.patch

  cp ${srcdir}/config .config
}
```

Save and Close with <kbd>CTRL</kbd> + <kbd>X</kbd>, then save with <kbd>Y</kbd>.

- To compile and package the kernel, run:
```
makepkg -si
```

# 3. Compiling Device Trees and Overlays

A complete guide for using `dtsc`, the BredOS tool for compiling DTB and DTBOs is now available. Click [here](/Tools#dtsc-helper-script) to view it.

# 4. Table of branches

| Branch | Target Architecture | Target SBCs | Source base |
|-------|-------|--------|--------|
| rk6.1-rkr3 | ARM64 | all RK35xx based SBCs | rkr3 Rockchip 6.1 |
| rk-mainline | ARM64 | all RK35xx based SBCs | linux-next |
| k1-6.17.y | RISC-V | all Spacemit K1/M1 based SBCs | linux-6.17 |
| k1-6.15.y | RISC-V | all Spacemit K1/M1 based SBCs | linux-6.15 |
| 6.18.y | x86_64 / ARM64 | all UEFI based devices | linux-next |
| 6.17.y | x86_64 / ARM64 | all UEFI based devices | linux-6.17 |
| 6.6.y-cix | ARM64 | all CIX CD81xx based SBCs | cix 6.6 |
| cix-acpi | ARM64 | all CIX CD81xx based SBCs | linux-next |
