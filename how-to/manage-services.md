---
title: How to manage services
description: 
published: false
date: 2025-10-01T10:13:28.737Z
tags: 
editor: markdown
dateCreated: 2025-09-30T10:31:51.284Z
---

# 1. Introduction
Managing services is a core part of administering a Linux system, and systemctl—part of the systemd suite—is the primary tool for the job on most modern distributions, including BredOS. Whether you need to start a service, stop it, check its status, or configure it to launch at boot, systemctl provides a consistent and powerful interface. This guide will walk you through the essential commands and practical examples to help you take control of system services with confidence.

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

- A `exited` service is one that runs at boot, performs its task, and then terminates cleanly. A good example of this is the systemd-tmpfiles-setup service. It starts on boot, sets up a ramdisk, mounts it to /tmp, and then exits gracefully.

- A `failed` service did not start correctly or encountered a problem while running and stopped with an error code. This does not mean that your system is broken, but fixing it might still be advisable.

It is also possible to check the status of a given service, which provides more output, including its error message, if it has failed.
- To check the status of a given service run:
```
systemctl status <your service name here>
```

- For example, here is the output of a failed service containing its problem:
```
● nordvpnd.service - NordVPN Daemon
     Loaded: loaded (/usr/lib/systemd/system/nordvpnd.service; enabled; preset: disabled)
     Active: activating (auto-restart) (Result: exit-code) since Fri 2025-09-26 12:53:07 CEST; 3s ago
 Invocation: adf87be78f8b44e3ba66a18268b87241
TriggeredBy: ● nordvpnd.socket
    Process: 1916 ExecStart=/usr/sbin/nordvpnd (code=exited, status=127)
   Main PID: 1916 (code=exited, status=127)
   Mem peak: 2M
        CPU: 28ms

Sep 26 12:53:13 bredos systemd[1]: nordvpnd.service: Scheduled restart job, restart counter is at 1.
Sep 26 12:53:13 bredos systemd[1]: Stopped NordVPN Daemon.
Sep 26 12:53:13 bredos systemd[1]: Started NordVPN Daemon.
Sep 26 12:53:13 bredos nordvpnd[1971]: /usr/sbin/nordvpnd: error while loading shared libraries: libxml2.so.2: cannot open shared object file: No such file or directory
Sep 26 12:53:13 bredos systemd[1]: nordvpnd.service: Main process exited, code=exited, status=127/n/a
Sep 26 12:53:13 bredos systemd[1]: nordvpnd.service: Failed with result 'exit-code'.
```

In the given example above, the nordvpnd service failed to start because it is missing the library libxml2.so.2. With this information, it is easily fixable.

# 3. Manage services
Services can be started and/or stopped manually or at boot. To manage the behaviour of a service do the following.

- To start a service manually, run:
```
sudo systemctl start <your service name here>
```

- And to stop it, run:
```
sudo systemctl stop <your service name here>
```

The logic continues with activating and deactivating services on boot. Use `systemctl enable` to start them on boot, or `systemctl disable` to prevent them from starting on boot. With the parameter `--now`, you can start and activate them at the same time.

- For example, if you want to activate nordvpnd on boot and start it with the same command, run:
```
sudo systemctl enable --now nordvpnd
```

# 4. Edit and create services
It is also possible to edit or create services to your liking. System-wide service-files, which come through a package installation, are typically stored in `/usr/lib/systemd/system`, or `/etc/systemd/system`, while user-wide service-files are stored in `~/.config/systemd/user`, or `/etc/systemd/user`.

- To create a system-wide service-file, run:
```
sudo nano /etc/systemd/system/<your service-file name here>
```

- Then fill the newly created file with some info. For example:
```
[Unit]
Description=Run my one-shot script at startup
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/my-oneshot-script.sh
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```

This service-file will run /usr/local/bin/my-oneshot-script.sh and go into the state `exited` after the script terminates cleanly. 

- To edit a existing service, run:
```
sudo systemctl edit <your service-file name here>
```

> Please be aware that editing service-files **can** be dangerous!
{.is-danger}

- After you edited a service-file you need to reload the syystemd-daemon:
```
sudo systemctl daemon-reload
```


