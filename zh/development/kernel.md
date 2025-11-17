---
title: 内核moding
description:
published: true
date: 2025-11-17T08:42:44.282Z
tags:
editor: markdown
dateCreated: 2024-11T11:49:44.206Z
---

# 4. 重要目录

本指南主要侧重于RK3588 和 linux-rockchip-rkr3 内核； 然而，一般进程和许多概念也应适用于其他内核和装置。 您是否正在开发自定义固件，有助于上游内核支持。 或只是设法了解Linux内核是如何为硬件构建的，本条旨在提供一个明确和实际的出发点。

# 2. BredOS kernel PKGBUILD

## BredOS 内核仓库

BredOS 在 [https://github.com/BredOS/linux-bredos](https://github.com/BredOS/linux-bredos) 存储它的 `linux-rockchip` 内核叉。

用于rkr3内核的分支是 `rk6.1-rkr3`，主线变量则在 `rk-mainline` 处。

> 查看[branches的表格](#h-211-table-of-branches) 来找出您设备要使用的分支。
> {.is-info}

### 2.1.1 分行表

| 分支                                        | 目标结构                                | Target SBCs          | 源代码基础                             | PKGBUILD 名称                                   |
| ----------------------------------------- | ----------------------------------- | -------------------- | --------------------------------- | --------------------------------------------- |
| rk6.1-rkr3                | ARM64                               | 所有基于 RK35xx 的 SBC    | rkr3 Rockchip 6.1 | linux-rockchip-rkr3                           |
| rk-主线                                     | ARM64                               | 所有基于 RK35xx 的 SBC    | 下一个 linux                         | linux-rockchip-mainline                       |
| k1-6.17.y | RISC-V                              | 所有空格 K1/M1 基于 SBC    | linux-6.17        | linux-spacemit-k1                             |
| k1-6.15.y | RISC-V                              | 所有空格 K1/M1 基于 SBC    | linux-6.15        | linux-spacemit-K1 (需要编辑分支) |
| 6.18.y    | x86_64 / ARM64 | 所有基于 UEFI 的设备        | 下一个 linux                         | linux                                         |
| 6.17.y    | x86_64 / ARM64 | 所有基于 UEFI 的设备        | linux-6.17        | linux (需要编辑分支)             |
| 6.6.y-cix | ARM64                               | 所有 CIX CD81xx 基于 SBC | cix 6.6           | 无                                             |
| ix-acpi                                   | ARM64                               | 所有 CIX CD81xx 基于 SBC | 下一个 linux                         | 无                                             |
| {.dense}                  |                                     |                      |                                   |                                               |

## 2.2 Building BredOS 内核

就像任何自定义的 BredOS PKGBUILD一样，内核也可以在 [https://github.com/BredOS/sbc-pkgbuilds](https://github.com/BredOS/sbc-pkgbuilds)找到。 在这个示例中，我们生成rkr3内核，但本指南适用于我们仓库中发现的所有Linux内核PKGBUILD。

- 复制资源库：

```
git clone https://github.com/BredOS/sbc-pkgbuilding
```

这将创建一个名为`sbc-pkgbuilds`的文件夹，在当前目录中保存我们仓库中的任何自定义包，包括内核PKGBUILD。

- 更改内核PKGBUILD目录：

```
cd sbc-pkgbuils
cd linux-rockchip-rkr3
```

- 该文件夹的内容应如下：

```
PKGBUILD
bredos-update-dtbs
config
dtb-update.hook
linux.preset
```

- 要编译和打包内核，请运行：

```
毫克-西文
```

> 虽然参数 `-s` 会自动安装所有必要的依赖关系，但参数 `-i` 会在编译成功后安装包。
> {.is-info}

## 2.3 用补丁构建内核。

要用补丁构建内核，我们需要实现补丁到PKGBUILD。 Follow the section [2.2 Building BredOS Kernel](/en/development/kernel#h-2-2-building-bredos-kernel) but dont run the command `makepkg -si` yet.

- 这是补丁的示例代码：

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

> 这个示例补丁设置了一个固定的名称，而不是生成给您编译的内核。
> {.is-info}

保存您的补丁到文件`PKGBUILD`旁边的.patch文件。 在这个示例中，我们将以上代码保存为 `example.patch` 。

- 要实现补丁到PKGBUILD，请运行：

```
nano PKGBUILD
```

- 查看 "Prepare" 部分。 看起来像这样：

```
prepare() {
  cd linux-bredos

  cp ${srcdir}/config .config
}
```

- 并在“cd linux-bredos”之后添加您的补丁：

```
prepare() {
  cd linux-bredos

  git apply ../../example.patch

  cp ${srcdir}/config .config
}
```

使用 <kbd>CTRL</kbd> + <kbd>X</kbd>保存并关闭，然后使用 <kbd>Y</kbd> 保存。

- 要编译和打包内核，请运行：

```
毫克-西文
```

# 3. 编译设备树和叠加

使用`dtsc`、BredOS工具编译DTB和DTBO的完整指南现已可供使用。
点击 [here]/Tools#dtsc-helper-script) 查看它。 Click [here](/Tools#dtsc-helper-script) to view it.

