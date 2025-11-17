---
title: Kernel modding
description: 
published: true
date: 2025-11-17T11:00:32.207Z
tags: 
editor: markdown
dateCreated: 2024-11-11T11:49:44.206Z
---

# 1. Introduction

This guide primarily focuses on RK3588 and the linux-rockchip-rkr3 kernel; however, the general process and many of the concepts should also apply to other kernels and devices. Whether you are developing custom firmware, contributing to upstream kernel support, or simply seeking to understand how the Linux kernel is built for hardware, this article aims to provide a clear and practical starting point.


# 2. Obtaining the kernel or it's source code
## 2.1 BredOS kernel Repository

BredOS stores it's `linux-rockchip` kernel fork at [https://github.com/BredOS/linux-bredos](https://github.com/BredOS/linux-bredos).

The branch used for the rkr3 kernel is `rk6.1-rkr3`, the mainline variant is instead at `rk-mainline`. 

> Check out the [table of branches](#h-211-table-of-branches) to find out which branch to use for your device.
{.is-info}

### 2.1.1 Table of branches

| Branch | Target Architecture | Target SBCs | Source base | PKGBUILD name |
|-------|-------|--------|--------|--------|
| [rk6.1-rkr3](https://github.com/BredOS/linux-bredos/tree/rk6.1-rkr3) | ARM64 | all RK35xx based SBCs | rkr3 Rockchip 6.1 | [linux-rockchip-rkr3](https://github.com/BredOS/sbc-pkgbuilds/tree/main/linux-rockchip-rkr3) |
| [rk-mainline](https://github.com/BredOS/linux-bredos/tree/rk-mainline) | ARM64 | all RK35xx based SBCs | linux-next | [linux-rockchip-mainline](https://github.com/BredOS/sbc-pkgbuilds/tree/main/linux-rockchip-mainline) |
| [k1-6.17.y](https://github.com/BredOS/linux-bredos/tree/k1-6.17.y) | RISC-V | all Spacemit K1/M1 based SBCs | linux-6.17 | [linux-spacemit-k1](https://github.com/BredOS/sbc-pkgbuilds/tree/main/linux-spacemit-k1) |
| [k1-6.15.y](https://github.com/BredOS/linux-bredos/tree/k1-6.15.y) | RISC-V | all Spacemit K1/M1 based SBCs | linux-6.15 | linux-spacemit-k1 (need to edit branch) |
| [6.18.y](https://github.com/BredOS/linux-bredos/tree/6.18.y) | x86_64 / ARM64 | all UEFI based devices | linux-next | [linux](https://github.com/BredOS/sbc-pkgbuilds/tree/main/linux) |
| [6.17.y](https://github.com/BredOS/linux-bredos/tree/6.17.y) | x86_64 / ARM64 | all UEFI based devices | linux-6.17 | linux (need to edit branch) |
| [6.6.y-cix](https://github.com/BredOS/linux-bredos/tree/6.6.y-cix) | ARM64 | all CIX CD81xx based SBCs | cix 6.6 | N/A |
| [cix-acpi](https://github.com/BredOS/linux-bredos/tree/cix-acpi) | ARM64 | all CIX CD81xx based SBCs | linux-next | N/A |
{.dense}

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

> The tool `makepkg` downloads the source code into `./src/linux-bredos`. Since we have stored the patch file next to the PKGBUILD, the path to our patch file must include `../../`.
{.is-info}

Save and Close with <kbd>CTRL</kbd> + <kbd>X</kbd>, then save with <kbd>Y</kbd>.

- To compile and package the kernel, run:
```
makepkg -si
```

# 3. Compiling Device Trees and Overlays

A complete guide for using `dtsc`, the BredOS tool for compiling DTB and DTBOs is now available. Click [here](/Tools#dtsc-helper-script) to view it.

