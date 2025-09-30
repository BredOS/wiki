---
title: How to manage services
description: 
published: false
date: 2025-09-30T10:31:51.284Z
tags: 
editor: markdown
dateCreated: 2025-09-30T10:31:51.284Z
---

# 1. Introduction
Managing services is a core part of administering a Linux system, and systemctl—part of the systemd suite—is the primary tool for the job on most modern distributions. Whether you need to start a service, stop it, check its status, or configure it to launch at boot, systemctl provides a consistent and powerful interface. This guide will walk you through the essential commands and practical examples to help you take control of system services with confidence.

# 2. Examine your services
## 2.1 With `bredos-news`
- The tool `bredos-news` automatically starts whenever you open the command line.

![bredos-news.png](/systemd/bredos-news.png)

At the end of its output, you can read the text "System is operating normally." This means that all services supposed to start on boot have been started without any error. If you have just booted your device, it may show the warning "PLEASE ADD WARNING HERE." This is normal, as many services can be started in parallel, which can lead to delays while starting. This warning should go away after a few minutes.

If you see the error message, "PLEASE ADD ERROR MESSAGE HERE," one or more services have failed to start. To identify the issue with the service and potentially fix it, continue with Section 3.

## 2.2 With `systemctl`
- To list all services on your computer run:
```
systemctl list-units --type=service
```

This outputs a list of services. Navigate though it with your arrow keys, or use <kbd>space</kbd> to go one page down. Leave it with the <kbd>Q</kbd> key. 

Services can have different states as shown in the row "SUB". They can be `running`, `exited`, or `failed`.

- A `running` service performs background tasks for you. A great example of this is Network Manager. This service manages your network connectivity. Since you can always plug in an Ethernet cable, the program needs to run continuously to manage your network accordingly. This is achieved by a `running` service.

- An `exited` service is one that runs at boot, performs its task, and then terminates cleanly. A good example of this is the systemd-tmpfiles-setup service. It starts on boot, sets up a ramdisk, mounts it to /tmp, and then exits gracefully.

- A `failed` service did not start correctly or encountered a problem while running and stopped with an error code. This does not mean that your system is broken, but fixing it might still be advisable.

