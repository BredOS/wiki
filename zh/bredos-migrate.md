---
title: BredOS-Migrate
description: A script to migrate your BredOS installation
published: false
date: 2025-12-14T11:34:10.351Z
tags:
editor: markdown
dateCreated: 2025-12-14T11:34:10.351Z
---

# 1. Introduction

The tool `bredos-migrate` is a script to migrate an installation of BredOS to different boot media. The source to migrate from can either be your currently booted BredOS installation, an installation of BredOS on a connected storage device, or directly from an image file.
The script handles the change in UUIDs, flashing the correct bootloader, and copying all needed files from the source.

> This script has been barely tested. Use it only if you have been specifically advised to do so!
> {.is-danger}

# 2. Usage

## 2.1 Migrate your booted installation

- To migrate your currently booted installation, run:

```
bredos-migrate --destination-drive <path to drive here>
```

- Output should be as follows:

```
Detecting Image type ...
Source Part 1 info: <path to source drive> vfat <bootfs UUID>
Source Part 2 info: <path to source drive> btrfs <rootfs UUID>
Source Drive: <path to source drive>
Destination Drive: <path to destination drive>
Detected bootloader: <the detected bootloader from source drive>

If you continue all data will be deleted on drive <path to destination drive>!
Are you sure to continue? [y/N] y
Creating partition table on <path to destination drive> ...
Formating partitions ...
Creating subvolumes ...
Mounting drives ...
Copy operating system files ...
Alter bootloader config ...
Alter filesystem table ...
Unmounting drives ...
Flash bootloader to <path to destination drive> ...
Finished!

```

## 2.2 Migrate from .img file

- To migrate from a image file, run:

```
bredos-migrate --destination-drive <path to drive here> --img <path to bred.img here>
```

## 2.3 Migrate from attached storage media

- To migrate from a attached storage media, run:

```
bredos-migrate --destination-drive <path to drive here> --source-drive <path to attached media here>
```

## 2.4 Advanced options

With the option `--hostname`, the given hostname will be set for the newly migrated installation.
With the option `--skip-home`, the home folder will not be copied over. Use this to speed up the process or if your target storage media is too small to hold all data from your source. Please be aware that you will need to create a home folder with the correct permissions after the migration; otherwise, you won't be able to log in as that user. However, root login should work without issues.
The option `--debug` enables printing of all command outputs directly to standard output (stdout) instead of creating a log file named `logfile.txt` in the current folder.