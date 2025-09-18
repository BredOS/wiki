---
title: 处理失败的磁盘
description: S. M.A.R.T 数据和更换磁盘的指南
published: true
date: 2025-09-15T09:04:50.217Z
tags:
editor: markdown
dateCreated: 2025-06-01T10:33:55.798Z
---

# 1. 重要标签

本指南是从个人经历中收集到的一系列建议。
在执行本指南中的任何命令时确保正确的理解和风险。
数据丢失是可能的。

> **不**信任聊天GPT或任何其他恢复失败的磁盘的LM。 你将会失望！
> {.is-danger}

# 2. 报告失败

BredOS 新闻服务现在将报告连接的驱动器失败或损坏，并且提供了 S.M.A.R.T 数据。

如果您已经从BredOS News链接到这个部分，头部到下面的部分。

```失败\~\~
```

> 这一部分正在建造中。 请通过 Discord 或 Telegram 联系我们 - 我们很乐意提供帮助 ！
> {.is-warning}

# 3. S.M.A.R.T 数据

## 3.1 查看S.M.A.R.T Data (HDD)

- 假设硬盘 `/dev/sda`，查看它的 S.M.A.R.T 数据，运行：

```
sudo smartctl -a /dev/sda
```

- 这将印制一份大量报告：

```
smartctl 7.5 2025-04-30 r5714 [aarch64-linux-6.1.44-1-sky1] (local build)
Copyright (C) 2002-25, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF INFORMATION SECTION ===
Model Family:     Toshiba 3.5" DT01ACA... Desktop HDD
Device Model:     TOSHIBA DT01ACA050
Serial Number:    X5NGNE1GS
LU WWN Device Id: 5 000039 fe4d4c15b
Firmware Version: MS1OA750
User Capacity:    500,107,862,016 bytes [500 GB]
Sector Sizes:     512 bytes logical, 4096 bytes physical
Rotation Rate:    7200 rpm
Form Factor:      3.5 inches
Device is:        In smartctl database 7.5/5706
ATA Version is:   ATA8-ACS T13/1699-D revision 4
SATA Version is:  SATA 3.0, 6.0 Gb/s (current: 6.0 Gb/s)
Local Time is:    Sun Jun  1 13:03:14 2025 EEST
SMART support is: Available - device has SMART capability.
SMART support is: Enabled

=== START OF READ SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED

General SMART Values:
Offline data collection status:  (0x84)	Offline data collection activity
					was suspended by an interrupting command from host.
					Auto Offline Data Collection: Enabled.
Self-test execution status:      (   0)	The previous self-test routine completed
					without error or no self-test has ever 
					been run.
Total time to complete Offline 
data collection: 		( 3498) seconds.
Offline data collection
capabilities: 			 (0x5b) SMART execute Offline immediate.
					Auto Offline data collection on/off support.
					Suspend Offline collection upon new
					command.
					Offline surface scan supported.
					Self-test supported.
					No Conveyance Self-test supported.
					Selective Self-test supported.
SMART capabilities:            (0x0003)	Saves SMART data before entering
					power-saving mode.
					Supports SMART auto save timer.
Error logging capability:        (0x01)	Error logging supported.
					General Purpose Logging supported.
Short self-test routine 
recommended polling time: 	 (   1) minutes.
Extended self-test routine
recommended polling time: 	 (  59) minutes.
SCT capabilities: 	       (0x003d)	SCT Status supported.
					SCT Error Recovery Control supported.
					SCT Feature Control supported.
					SCT Data Table supported.

SMART Attributes Data Structure revision number: 16
Vendor Specific SMART Attributes with Thresholds:
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
  1 Raw_Read_Error_Rate     0x000b   100   100   016    Pre-fail  Always       -       0
  2 Throughput_Performance  0x0005   142   142   054    Pre-fail  Offline      -       71
  3 Spin_Up_Time            0x0007   126   126   024    Pre-fail  Always       -       184 (Average 181)
  4 Start_Stop_Count        0x0012   100   100   000    Old_age   Always       -       117
  5 Reallocated_Sector_Ct   0x0033   100   100   005    Pre-fail  Always       -       0
  7 Seek_Error_Rate         0x000b   100   100   067    Pre-fail  Always       -       0
  8 Seek_Time_Performance   0x0005   110   110   020    Pre-fail  Offline      -       36
  9 Power_On_Hours          0x0012   091   091   000    Old_age   Always       -       65606
 10 Spin_Retry_Count        0x0013   100   100   060    Pre-fail  Always       -       0
 12 Power_Cycle_Count       0x0032   100   100   000    Old_age   Always       -       115
192 Power-Off_Retract_Count 0x0032   100   100   000    Old_age   Always       -       196
193 Load_Cycle_Count        0x0012   100   100   000    Old_age   Always       -       196
194 Temperature_Celsius     0x0002   139   139   000    Old_age   Always       -       43 (Min/Max 19/49)
196 Reallocated_Event_Count 0x0032   100   100   000    Old_age   Always       -       0
197 Current_Pending_Sector  0x0022   100   100   000    Old_age   Always       -       0
198 Offline_Uncorrectable   0x0008   100   100   000    Old_age   Offline      -       0
199 UDMA_CRC_Error_Count    0x000a   200   200   000    Old_age   Always       -       0

SMART Error Log Version: 1
No Errors Logged

SMART Self-test log structure revision number 1
No self-tests have been logged.  [To run self-tests, use: smartctl -t]

SMART Selective self-test log data structure revision number 1
 SPAN  MIN_LBA  MAX_LBA  CURRENT_TEST_STATUS
    1        0        0  Not_testing
    2        0        0  Not_testing
    3        0        0  Not_testing
    4        0        0  Not_testing
    5        0        0  Not_testing
Selective self-test flags (0x0):
  After scanning selected spans, do NOT read-scan remainder of disk.
If Selective self-test is pending on power-up, resume after 0 minute delay.

The above only provides legacy SMART information - try 'smartctl -x' for more
```

在所有这些情况下，下列数据对于寻找：

- “SMART overall health 自我评估”，应为“PASSED”。 如果报告了任何其他值，应将驱动器替换为急速。 如果报告了任何其他值，应将驱动器替换为急速。
- `重新分配Sector_Ct`，重新安置区的数目，如果一个以上的区域显示级联失败的可能性很大。

## 3.2 查看S.M.A.R.T Data (NVME)

- 假设NVME `/dev/nvme0`，查看它的 S.M.A.R.T 数据，运行：

```
sudo smartctl -a /dev/nvme0
```

- 假设NVME 支持 S.M.A.R.T，这将打印一个小报告：

```
smartctl 7.5 2025-04-30 r5714 [aarch64-linux-6.1.44-1-sky1] (local build)
Copyright (C) 2002-25, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF INFORMATION SECTION ===
Model Number:                       ADATA LEGEND 710
Serial Number:                      2O252LASS72J
Firmware Version:                   VC2SAD01
PCI Vendor/Subsystem ID:            0x1cc1
IEEE OUI Identifier:                0x707c18
Controller ID:                      1
NVMe Version:                       1.4
Number of Namespaces:               1
Namespace 1 Size/Capacity:          256,060,514,304 [256 GB]
Namespace 1 Formatted LBA Size:     512
Namespace 1 IEEE EUI-64:            707c18 0c83eec2e9
Local Time is:                      Sun Jun  1 13:08:13 2025 EEST
Firmware Updates (0x02):            1 Slot
Optional Admin Commands (0x0017):   Security Format Frmw_DL Self_Test
Optional NVM Commands (0x005e):     Wr_Unc DS_Mngmt Wr_Zero Sav/Sel_Feat Timestmp
Log Page Attributes (0x02):         Cmd_Eff_Lg
Maximum Data Transfer Size:         32 Pages
Warning  Comp. Temp. Threshold:     100 Celsius
Critical Comp. Temp. Threshold:     110 Celsius

Supported Power States
St Op     Max   Active     Idle   RL RT WL WT  Ent_Lat  Ex_Lat
 0 +     8.00W       -        -    0  0  0  0   230000   50000
 1 +     4.00W       -        -    1  1  1  1     4000   50000
 2 +     3.00W       -        -    2  2  2  2     4000  250000
 3 -   0.0300W       -        -    3  3  3  3     5000   10000
 4 -   0.0050W       -        -    4  4  4  4    54000   45000

Supported LBA Sizes (NSID 0x1)
Id Fmt  Data  Metadt  Rel_Perf
 0 +     512       0         0

=== START OF SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED

SMART/Health Information (NVMe Log 0x02, NSID 0xffffffff)
Critical Warning:                   0x00
Temperature:                        35 Celsius
Available Spare:                    100%
Available Spare Threshold:          32%
Percentage Used:                    0%
Data Units Read:                    840,013 [430 GB]
Data Units Written:                 1,699,047 [869 GB]
Host Read Commands:                 7,031,574
Host Write Commands:                25,090,339
Controller Busy Time:               0
Power Cycles:                       33
Power On Hours:                     229
Unsafe Shutdowns:                   23
Media and Data Integrity Errors:    0
Error Information Log Entries:      0
Warning  Comp. Temperature Time:    0
Critical Comp. Temperature Time:    0

Error Information (NVMe Log 0x01, 8 of 8 entries)
No Errors Logged

Self-test Log (NVMe Log 0x06, NSID 0xffffffff)
Self-test status: No self-test in progress
No Self-tests Logged
```

在这方面，唯一重要的价值观是：

- “使用的百分比”，即使用过的备件块的百分比。 它不应超过\`可用的Spare 阈值'，因为这通常是驱动器不返回的点。
  块失败率通常会通过该点呈指数增长，从而导致完全失败。
  NVME 驱动器可能会被锁定并在剩余闪光过期后开启只读功能。
- “介质和数据完整性错误”，表明有相当大的闪光度。
- `错误信息记录条目`, 通常表明有多少闪光区域被掩盖了零件刷入。

## 3.3 我应取代驱动器吗？

如果你只有少数(<5)移位区块，很可能会在一段时间内不再使用磁盘。
使用几个剩余的 nvme 闪屏块也是很好的。
使用几个剩余的 nvme 闪屏块也是很好的。

然而，通过剩余的闪光或迅速迁移，数十个区段被烧毁是即将失败的迹象。

由于剩余闪光或扇区耗尽，系统的性能将会迅速降解，文件系统像BTRFS 这样将被锁定。 拒绝执行以确保不会损坏磁盘。


