---
title: 如何管理服务
description:
published: false
date: 2025-10-01T11:12:56.618Z
tags:
editor: markdown
dateCreated: 2025-09-30T10:31:51.284Z
---

# 2. 介绍信息

管理服务是管理Linux系统的核心部分。 在包括BredOS在内的大多数现代分销系统中，主要的工作工具是系统配套系统的一部分。 是否需要启动服务，停止它，检查它的状态 或配置它以启动，systemctl 提供一个一致和强大的接口。 本指南将带着你去看基本的命令和实际示例来帮助你可靠地管理系统服务。

# 1. 检查您的服务

## 2.1 使用 `bredos-news`

- 当你打开命令行时，工具`bredos-news`自动启动。

![bredos-news.png](/systemd/bredos-news.png)

在输出结束时，您可以读取文本“系统正常运行”。 这意味着本应在启动时启动的所有服务已经启动，没有任何错误。 如果您刚刚启动了您的设备，它可能会显示警告“**X** 服务报告状态激活”。这是正常的， 许多服务可以平行启动，这可能导致在启动时出现延误。 这种警告将在几分钟后消失。

如果您看到错误消息，"**X** 服务报告状态失败"一个或多个服务启动失败。 为了确定该处的问题并可能予以解决，继续第3节。

## 2.2 使用 `systemctl`

- 要列出您计算机上的所有全系统服务，请运行：

```
systemctl list-units --type=service
```

- 要列出您计算机上所有用户范围的服务，请运行：

```
systemctl list-units --type=service --user
```

此输出服务列表。 使用箭头键导航，或使用 <kbd>空间</kbd> 向下转一页。 用 <kbd>Q</kbd> 键退出

服务可以有不同的状态，如“SUB”行所示。 它们可以是 `running`, `exited`, 或 `failed`。

- 一个 `running' 服务为您执行背景任务。 一个很好的例子是网络管理员。 此服务管理您的网络连接。 既然你总是可以在以太网电缆中插入，程序需要连续运行以管理您的网络。 这是通过 `running\` 服务实现的。

- `exited`服务是在启动时运行，执行任务，然后全程终止。 一个很好的例子是系统-tmpfiles-setup 服务。 它从启动开始，建立一个斜杆，把它挂到/tmp，然后退出。

- “失败”服务在运行时未正确启动或遇到问题，并以错误代码停止。 这并不意味着你的系统已经崩溃，而是可能仍然需要修复它。

还可以检查给定服务的状态，如果它失败，它提供了更多的输出，包括错误消息。

- 要检查指定服务的状态：

```
systemctl 状态 <your service name here>
```

- 例如，这里是包含问题的服务失败的输出：

```
● nordvpnd.service - NordVPN 守护进程
     已载入：(/usr/lib/systemd/system/nordvpnd. ervice; 启用; 预设: 禁用)
     Active: 激活 (自动重启) (结果: 退出代码) 自Fri 2025-09-26 12:53:07; 3秒前
 调用： adf87be78f8b44e3ba66a18268b87241
触发： nordvpnd ocket
    Process: 1916 ExecStart=/usr/sbin/nordvpnd (Code=exed, status=127)
   Main PID: 1916 (Code=exed, status=127)
   平均峰值：2M
        CPU：28ms

Sep 26 12:53:13 bredos systemd[1]: nordvpnd ervice: 计划重启作业, 重启计数器为 1.
设置26 12:53:13 bredos systemd[1]: 停止NordVPN 守护程序。
Sep 26 12:53:13 bredos systemd[1]: Started NordVPN Daemon
Sep 26 12:53:13 bredos nordvpnd[1971]: /usr/sbin/nordvpnd: 加载共享库时出错: libxml2. o.2：无法打开共享对象文件：没有这样的文件或目录
Sep 26 12:53:13 bredos systemd[1]: nordvpnd ervice: Main process exist, code=exed, status=127/n/a
Sep 26 12:53:13 bredos systemd[1]: nordvpnd.service: failed with result 'exit-code'。
```

在上面给定的示例中，Nordvpnd 服务由于缺少库 libxml2.so.2 而无法启动。 有了这种信息，就很容易修复。

# 4. 管理服务

服务可以手动启动和/或停止，也可以在启动时停止。 管理一个服务的行为做以下事情。

- 手动启动服务，运行：

```
sudo systemctl start <your service name here>
```

- 要停止它，请运行：

```
sudo systemctl stop <your service name here>
```

启动时激活和停用服务的逻辑仍在继续。 使用 `systemctl enable` 来启动它们，或者 `systemctl disable` 来阻止它们在启动时启动。 使用参数 `--now `，您可以同时启动并激活它们。

- 例如，如果你想要在启动时激活 nordvpnd 并用相同的命令启动它，请运行：

```
sudo systemctl 启用 --now nordvpnd
```

# 🚀 4. 编辑和创建服务

它也可以根据您的喜好编辑或创建服务。 全系统服务文件通常存储在`/usr/lib/systemd/system`或`/etc/systemd/system`中，而全用户范围的服务文件则存储在`~/.config/systemd/user`或`/etc/systemd/user`中。

- 要创建全系统服务文件，请运行：

```
sudo nano /etc/systemd/system/<your service-file name here>.service
```

- 然后用一些信息填写新创建的文件。 例如：

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

此服务文件将运行 /usr/local/bin/my-oneshot-script.sh 并在脚本全部终止后输入状态“exited”。

- 要编辑现有的服务，请运行：

```
sudo systemctl edit <your service-file name here>
```

> 请注意编辑服务文件 **可以** 危险！
> {.is-danger}

- 在您编辑服务文件后，您需要重新加载系统系统：

```
sudo systemctl 守护进程重载
```

# 🔄 3. 作弊表

许多linux disruubiutions 发布系统的作弊单。 由于它们基本上是一样的，所以我们提供了一个链接到[Red Hat's Cheat Sheet for system](https://access.redhat.com/sites/default/files/attachments/12052018_systemd_6.pdf)。
