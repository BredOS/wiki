---
title: 处理失败的磁盘
description: S. M.A.R.T 数据和更换磁盘的指南
published: true
date: 2025-09-23T15：33：58.026Z
tags:
editor: markdown
dateCreated: 2025-06-01T10:33:55.798Z
---

# 1. 重要标签

本指南是从个人经历中收集到的一系列建议。 在执行本指南中的任何命令时，您需要确保正确的理解和风险。 **数据丢失是可能的并可能的。**

> **不**信任聊天室或恢复失败的磁盘的任何其他LM。
> 你将会失望！ 使情况更糟始终是可能的。
> {.is-danger}
> 你将会失望！ 使情况更糟始终是可能的。
> {.is-danger}

# 2. 报告失败

在BredOS, 我们拒绝让任何用户遭受数据丢失。 仔细阅读这篇文章；如果您需要进一步的帮助，请随时在我们的支持频道或通过邮件联系我们。 仔细阅读这篇文章；如果您需要进一步的帮助，请随时在我们的支持频道或通过邮件联系我们。

- [📱 Telegram](https://t.me/bredoslinux)
- [💬 Discord](https://discord.gg/jwhuyKXaa)
- [Email](mailto:support@bredos.org)
  {.links-list}

# 3. 报告失败

BredOS 新闻服务现在将报告附加的已退化驱动程序。
(这只适用于那些报告 S.M.A.R.T.
(这只适用于那些报告 S.M.A.R.T. 的驱动程序。) 经常预算： 预算外：

如果您已经从BredOS News链接到这个部分，头部到下面的部分。

# 🚀 4. S.M.A.R.T 数据

## 查看S.M.A.R.T 数据 (HDD)

> 如果您有一个不同的存储介质，请在下面的头部到它的相关部分。
> 每一个都有自己的部分。
> {.is-info}
> {.is-info}

- 假设硬盘 `/dev/sda`，查看它的 S.M.A.R.T 数据，运行：

```
sudo smartctl -a /dev/sda
```

- 这将印制一份大量报告：

```
[bill88t@prion | ~]> sudo smartctl -a /dev/sda
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

这些数据大多与推动健康无关。 基于所有这些，你应该寻找：

- “SMART overall health 自我评估”，应为“PASSED”。 如果报告了任何其他值，应将驱动器替换为急速。 如果报告了任何其他值，应将驱动器替换为急速。
- `重新分配Sector_Ct`，重新安置区的数目，如果一个以上的区域显示级联失败的可能性很大。

## 查看S.M.A.R.T Data (NVME)

- 假设NVME `/dev/nvme0`，查看它的 S.M.A.R.T 数据，运行：

```
sudo smartctl -a /dev/nvme0
```

- 假设NVME 支持 S.M.A.R.T，这将打印一个小报告：

```
[bill88t@prion | ~]> sudo smartctl -a /dev/nvme0
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

## 3.3 查看EMMC的健康

> 不要在SD卡上运行此操作，它会崩溃它们。
> 它不会损害他们，但它不会做任何有益的事情。 它不会损害他们，但它不会做任何有益的事情。
> {.is-info} 它不会损害他们，但它不会做任何有益的事情。
> {.is-info}

- 假定`/dev/mmcblk0`，要查看它的控制器数据，请运行：

```
sudo mc extcsd read /dev/mmcblk0
```

- 这将返回许多数据：

```
=============================================
  Extended CSD rev 1.8 (MMC 5.1)
=============================================

Card Supported Command sets [S_CMD_SET: 0x01]
HPI Features [HPI_FEATURE: 0x01]: implementation based on CMD13
Background operations support [BKOPS_SUPPORT: 0x01]
Max Packet Read Cmd [MAX_PACKED_READS: 0x20]
Max Packet Write Cmd [MAX_PACKED_WRITES: 0x20]
Data TAG support [DATA_TAG_SUPPORT: 0x01]
Data TAG Unit Size [TAG_UNIT_SIZE: 0x00]
Tag Resources Size [TAG_RES_SIZE: 0x00]
Context Management Capabilities [CONTEXT_CAPABILITIES: 0x78]
Large Unit Size [LARGE_UNIT_SIZE_M1: 0x01]
Extended partition attribute support [EXT_SUPPORT: 0x03]
Generic CMD6 Timer [GENERIC_CMD6_TIME: 0x05]
Power off notification [POWER_OFF_LONG_TIME: 0x64]
Cache Size [CACHE_SIZE] is 128 KiB
Background operations status [BKOPS_STATUS: 0x00]
1st Initialisation Time after programmed sector [INI_TIMEOUT_AP: 0x0a]
Power class for 52MHz, DDR at 3.6V [PWR_CL_DDR_52_360: 0x00]
Power class for 52MHz, DDR at 1.95V [PWR_CL_DDR_52_195: 0x00]
Power class for 200MHz at 3.6V [PWR_CL_200_360: 0x00]
Power class for 200MHz, at 1.95V [PWR_CL_200_195: 0x00]
Minimum Performance for 8bit at 52MHz in DDR mode:
 [MIN_PERF_DDR_W_8_52: 0x00]
 [MIN_PERF_DDR_R_8_52: 0x00]
TRIM Multiplier [TRIM_MULT: 0x02]
Secure Feature support [SEC_FEATURE_SUPPORT: 0x55]
Boot Information [BOOT_INFO: 0x07]
 Device supports alternative boot method
 Device supports dual data rate during boot
 Device supports high speed timing during boot
Boot partition size [BOOT_SIZE_MULTI: 0x20]
Access size [ACC_SIZE: 0x06]
High-capacity erase unit size [HC_ERASE_GRP_SIZE: 0x01]
 i.e. 512 KiB
High-capacity erase timeout [ERASE_TIMEOUT_MULT: 0x02]
Reliable write sector count [REL_WR_SEC_C: 0x01]
High-capacity W protect group size [HC_WP_GRP_SIZE: 0x20]
 i.e. 16384 KiB
Sleep current (VCC) [S_C_VCC: 0x07]
Sleep current (VCCQ) [S_C_VCCQ: 0x07]
Sleep/awake timeout [S_A_TIMEOUT: 0x12]
Sector Count [SEC_COUNT: 0x1d200000]
 Device is block-addressed
Minimum Write Performance for 8bit:
 [MIN_PERF_W_8_52: 0x00]
 [MIN_PERF_R_8_52: 0x00]
 [MIN_PERF_W_8_26_4_52: 0x00]
 [MIN_PERF_R_8_26_4_52: 0x00]
Minimum Write Performance for 4bit:
 [MIN_PERF_W_4_26: 0x00]
 [MIN_PERF_R_4_26: 0x00]
Power classes registers:
 [PWR_CL_26_360: 0x00]
 [PWR_CL_52_360: 0x00]
 [PWR_CL_26_195: 0x00]
 [PWR_CL_52_195: 0x00]
Partition switching timing [PARTITION_SWITCH_TIME: 0x04]
Out-of-interrupt busy timing [OUT_OF_INTERRUPT_TIME: 0x0a]
I/O Driver Strength [DRIVER_STRENGTH: 0x1f]
Card Type [CARD_TYPE: 0x57]
 HS400 Dual Data Rate eMMC @200MHz 1.8VI/O
 HS200 Single Data Rate eMMC @200MHz 1.8VI/O
 HS Dual Data Rate eMMC @52MHz 1.8V or 3VI/O
 HS eMMC @52MHz - at rated device voltage(s)
 HS eMMC @26MHz - at rated device voltage(s)
CSD structure version [CSD_STRUCTURE: 0x02]
Command set [CMD_SET: 0x00]
Command set revision [CMD_SET_REV: 0x00]
Power class [POWER_CLASS: 0x00]
High-speed interface timing [HS_TIMING: 0x03]
Enhanced Strobe mode [STROBE_SUPPORT: 0x01]
Erased memory content [ERASED_MEM_CONT: 0x00]
Boot configuration bytes [PARTITION_CONFIG: 0x00]
 Not boot enable
 No access to boot partition
Boot config protection [BOOT_CONFIG_PROT: 0x00]
Boot bus Conditions [BOOT_BUS_CONDITIONS: 0x00]
High-density erase group definition [ERASE_GROUP_DEF: 0x01]
Boot write protection status registers [BOOT_WP_STATUS]: 0x00
Boot Area Write protection [BOOT_WP]: 0x00
 Power ro locking: possible
 Permanent ro locking: possible
 partition 0 ro lock status: not locked
 partition 1 ro lock status: not locked
User area write protection register [USER_WP]: 0x00
FW configuration [FW_CONFIG]: 0x00
RPMB Size [RPMB_SIZE_MULT]: 0x20
Write reliability setting register [WR_REL_SET]: 0x1f
 user area: the device protects existing data if a power failure occurs during a write operation
 partition 1: the device protects existing data if a power failure occurs during a write operation
 partition 2: the device protects existing data if a power failure occurs during a write operation
 partition 3: the device protects existing data if a power failure occurs during a write operation
 partition 4: the device protects existing data if a power failure occurs during a write operation
Write reliability parameter register [WR_REL_PARAM]: 0x15
 Device supports writing EXT_CSD_WR_REL_SET
 Device supports the enhanced def. of reliable write
Enable background operations handshake [BKOPS_EN]: 0x02
H/W reset function [RST_N_FUNCTION]: 0x00
HPI management [HPI_MGMT]: 0x01
Partitioning Support [PARTITIONING_SUPPORT]: 0x07
 Device support partitioning feature
 Device can have enhanced tech.
Max Enhanced Area Size [MAX_ENH_SIZE_MULT]: 0x00136a
 i.e. 81428480 KiB
Partitions attribute [PARTITIONS_ATTRIBUTE]: 0x00
Partitioning Setting [PARTITION_SETTING_COMPLETED]: 0x00
 Device partition setting NOT complete
General Purpose Partition Size
 [GP_SIZE_MULT_4]: 0x000000
 [GP_SIZE_MULT_3]: 0x000000
 [GP_SIZE_MULT_2]: 0x000000
 [GP_SIZE_MULT_1]: 0x000000
Enhanced User Data Area Size [ENH_SIZE_MULT]: 0x000000
 i.e. 0 KiB
Enhanced User Data Start Address [ENH_START_ADDR]: 0x00000000
 i.e. 0 bytes offset
Bad Block Management mode [SEC_BAD_BLK_MGMNT]: 0x00
Periodic Wake-up [PERIODIC_WAKEUP]: 0x00
Program CID/CSD in DDR mode support [PROGRAM_CID_CSD_DDR_SUPPORT]: 0x01
...
Native sector size [NATIVE_SECTOR_SIZE]: 0x00
Sector size emulation [USE_NATIVE_SECTOR]: 0x00
Sector size [DATA_SECTOR_SIZE]: 0x00
1st initialization after disabling sector size emulation [INI_TIMEOUT_EMU]: 0x0a
Class 6 commands control [CLASS_6_CTRL]: 0x00
Number of addressed group to be Released[DYNCAP_NEEDED]: 0x00
Exception events control [EXCEPTION_EVENTS_CTRL]: 0x0000
Exception events status[EXCEPTION_EVENTS_STATUS]: 0x0000
Extended Partitions Attribute [EXT_PARTITIONS_ATTRIBUTE]: 0x0000
..
eMMC Firmware Version:
eMMC SECURE_WP_SUPPORT: 1
eMMC SECURE_WP_EN_STATUS: 0
eMMC Life Time Estimation A [EXT_CSD_DEVICE_LIFE_TIME_EST_TYP_A]: 0x01
eMMC Life Time Estimation B [EXT_CSD_DEVICE_LIFE_TIME_EST_TYP_B]: 0x01
eMMC Pre EOL information [EXT_CSD_PRE_EOL_INFO]: 0x01
Secure Removal Type [SECURE_REMOVAL_TYPE]: 0x3b
 information is configured to be removed using a vendor defined
 Supported Secure Removal Type:
  information removed by an erase of the physical memory
  information removed by an overwriting the addressed locations with a character followed by an erase
  information removed using a vendor defined
Command Queue Support [CMDQ_SUPPORT]: 0x01
Command Queue Depth [CMDQ_DEPTH]: 32
Command Enabled [CMDQ_MODE_EN]: 0x00
Note: CMDQ_MODE_EN may not indicate the runtime CMDQ ON or OFF.
Please check sysfs node '/sys/devices/.../mmc_host/mmcX/mmcX:XXXX/cmdq_en'
```

- 在所有这一切中，唯一与健康有关的信息是：

```
eMMC Life Time Estimation A [EXT_CSD_DEVICE_LIFE_TIME_EST_TYP_A]: 0x01
eMMC Life Time Estimation B [EXT_CSD_DEVICE_LIFE_TIME_EST_TYP_B]: 0x01
```

这一数值表明了一定比例的健康状况。

- `0x01`值表示使用了0-10%生命值。
  `0x01`值表示使用了0-10%生命值。
  `0x02`值表示使用了11-20%的生命值。
  值`0x03`表示所使用的 21%-30%。
  如此是第四个...
- `0x01`值表示使用了0-10%生命值。
  `0x02`值表示使用了11-20%的生命值。
  值`0x03`表示所使用的 21%-30%。
  如此是第四个...
- 值`0x03`表示所使用的 21%-30%。
  如此是第四个...
- 如此是第四个...

## 3.4 BTRFS 报告的数据

如果你使用的 USB，SD卡 ~~或软盘驱动器 ~，很遗憾无法获得正确的报告数据。

假定它是一个 BredOS 系统驱动器，它是使用 BTRFS 文件系统格式化的。 BTRFS 收集所有错误，可以提交完整的报告。 BTRFS 收集所有错误，可以提交完整的报告。 BTRFS 收集所有错误，可以提交完整的报告。

- 假设`/dev/mmcblk0p3`, 为MOUNTED, 运行：

```
sudo btrfs 设备状态 /dev/mmcblk0p3
```

- 这将返回：

```
[/dev/mmcblk0p3].write_io_errs 0
[/dev/mmcblk0p3].read_io_errs 0
[/dev/mmcblk0p3].flush_io_errs 0
[/dev/mmcblk0p3].corruption_errs 0
[/dev/mmmcblk0p3].generation_errs 0
```

如果其中任何一个值是非零值，介质可能为 **SIGNIFICANTLY** 降解。

## 我应该替换驱动器吗？

如果你只有少数(<5)移位区块，很可能会在一段时间内不再使用磁盘。
使用几个剩余的 nvme 闪屏块也是很好的。
使用几个剩余的 nvme 闪屏块也是很好的。

然而，通过剩余的闪光或迅速迁移，数十个区段被烧毁是即将失败的迹象。

由于剩余闪光或扇区耗尽，系统的性能将会迅速降解，文件系统像BTRFS 这样将被锁定。 拒绝执行写字，拒绝损坏磁盘。


