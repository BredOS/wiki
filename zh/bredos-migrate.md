---
title: BredOS-迁移
description: 迁移您的 BredOS 安装的脚本
published: false
date: 2025-12-14T11:34:10.351Z
tags:
editor: markdown
dateCreated: 2025-12-14T11:34:10.351Z
---

# 2. 介绍信息

工具`bredos-migrate`是一个将BredOS安装迁移到不同引导媒体的脚本。 要迁移的来源可以是您当前启动的 BredOS 安装， 在已连接的存储设备上或直接从图像文件中安装 BredOS 。
脚本处理UUID中的更改，刷入正确的引导器，并从源复制所有需要的文件。

> 此脚本几乎没有测试。 只有在你被明确建议这样做时才使用！
> {.is-danger}

# 3. 用法

## 2.1 迁移您启动的安装

- 要迁移您当前启动的安装，请运行：

```
bredos-migration --destination-drive <path to drive here>
```

- 产出应如下：

```
正在检测图像类型...
源第一部分信息： <path to source drive> vfat <bootfs UUID>
源第二部分信息： <path to source drive> btrfs <rootfs UUID>
源驱动器： <path to source drive>
目标驱动器： <path to destination drive>
检测到的引导器： <the detected bootloader from source drive>

如果您继续所有数据将在驱动器 <path to destination drive>上删除！
您确定要继续吗？[/N] y
在 <path to destination drive> 上创建分区表。 .
正在形成分区...
正在创建子卷...
挂载驱动器...
复制操作系统文件...
修改引导器配置 。.
更改文件系统表...
正在卸载驱动器...
Flash bootloader to <path to destination drive> ...
已完成！

```

## 2.2 从.img文件迁移

- 要从图像文件迁移，请运行：

```
bredos-migration --destination-drive <path to drive here> --img <path to bred.img here>
```

## 2.3 从附加存储媒体迁移

- 要从附加存储媒体迁移，请运行：

```
bredos-migration --destination-drive <path to drive here> --source-drich <path to attached media here>
```

## 2.4 高级选项

使用 "--hostname" 选项将为新迁移的安装设置给定的主机名。
使用 "--skip-home" 选项，不会复制主文件夹。 用它来加速进程，或如果您的目标存储媒体太小，无法保存来自您来源的所有数据。 请注意，您需要在迁移后创建具有正确权限的主文件夹； 否则您将无法以该用户的身份登录。 然而，根登录应该能够正常工作，没有问题。
选项`--debug` 允许将所有命令输出直接打印到标准输出(stdout)，而不是创建一个名为“logfile”的日志文件。 当前文件夹中的 xt\`。