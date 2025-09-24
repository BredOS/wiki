---
title: ディスクの処理に失敗しました
description: S.M.A.R.T データとディスクの交換に関するガイド
published: true
date: 2025-09-24T09:25:24.826Z
tags:
editor: markdown
dateCreated: 2025-06-01T10:33:55.798Z
---

# 1. 重要な免責事項

このガイドは個人的な経験から集められたヒントのセットです。 このガイドでコマンドを実行する際には、適切な理解とリスクを確保する必要があります。 **データ損失は可能であり、可能性があります。**

> **失敗したディスクを回復する際にChatGPTやその他のLLMを信頼しない** こと。
> あなたはがっかりするでしょう！ それを悪化させることは常に可能です。
> {.is-danger}
> あなたはがっかりするでしょう！ それを悪化させることは常に可能です。
> {.is-danger}

# 2. ヘルプしてください

BredOSでは、ユーザーにデータの損失を経験させることを拒否します。 この記事を注意深く読んでください; さらに助けが必要な場合は、私たちのサポートチャネルまたはメールでお気軽にお問い合わせください。

- [📱 Telegram](https://t.me/bredoslinux)
- [💬 Discord](https://discord.gg/jwhxuyKXaa)
- [Email](mailto:support@bredos.org)
  {.links-list}

# 3. 報告された失敗

BredOS News サービスは、添付されている劣化したドライブを報告します。
(これは、S.M.A.R.T を報告するドライブでのみ動作します。 データ)
(これは、S.M.A.R.T を報告するドライブでのみ動作します。 データ)

BredOS Newsからこれにリンクされている場合は、ストレージタイプの関連する以下のセクションを参照してください。

# 🚀 4. S.M.A.R.T データ

## 4.1 Viewing S.M.A.R.T Data (HDD)

> 別の記憶媒体がある場合は、以下のセクションを参照してください。
> それぞれに独自のセクションがあります。
> {.is-warning}

- ハード ディスク `/dev/sda` を仮定して、S.M.A.R.T データを表示します。

```
sudo smartctl -a /dev/sda
```

- 大きなレポートを印刷します：

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

このデータのほとんどは、健康を促進するためには関係ありません。 これらのすべての中で、あなたは次のように探す必要があります:

- `SMART overall-health self-assessment` は、「パスワード」である必要があります。 他の値が報告された場合は、ドライブは急いで交換する必要があります。
- `Reallocated_Sector_Ct` は、移転されたセクタの数です。これは、1 つ以上のセクタがあれば、カスケード失敗の重大なリスクを示します。

## 4.2 Viewing S.M.A.R.T Data (NVME)

- NVMe `/dev/nvme0` を仮定して、S.M.A.R.T データを表示します。

```
sudo smartctl -a /dev/nvme0
```

- NVMEがS.M.A.R.Tをサポートしていると仮定すると、次のような小さなレポートが出力されます。

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

ここで、唯一の重要な値は次のとおりです。

- `Percentage Used` (スペアブロックの使用率) 通常はドライブのリターンがないため、`Available Spare Threshold`を超えてはいけません。
  ブロック障害の発生率は通常、指数関数的に増加し、完全な障害につながります。
  NVMEドライブは、スペアフラッシュが起動されるとロックアップして読み取り専用にする可能性があります。
- 重要なフラッシュ度を示す`メディアとデータ整合性エラー`。
- `Error Information Log Entries` は通常、スペアフラッシュでマスクされたフラッシュ領域の数を示します。

## 4.3 Viewing EMMC health

> SDカードでこれを実行しないでください、それらはクラッシュします。
> それは彼らに損害を与えることはありませんが、それは生産的なことを行いません。 それは彼らに損害を与えることはありませんが、それは生産的なことを行いません。
> {.is-warning}

- `/dev/mmcblk0` を想定して、コントローラのデータを表示します。

```
sudo mmc extcsd read /dev/mmcblk0
```

- これは多くのデータを返します:

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

- この中で唯一の健康関連情報は以下の通りです:

```
eMMC寿命推定A [EXT_CSD_DEVICE_LIFE_TIME_EST_TYP_A]: 0x01
eMMC寿命推定B [EXT_CSD_DEVICE_LIFE_TIME_EST_TYP_B]: 0x01
```

この値は、健康のパーセンテージ範囲を示しています。

- 値 `0x01` は、0-10% の健康状態を示します。
  値 `0x02` は11-20% の健康状態を示します。
  値 `0x03` は、健康状態が21-30%であることを示します。
  そして、そしてその第四に
- 値 `0x02` は11-20% の健康状態を示します。
- 値 `0x03` は、健康状態が21-30%であることを示します。
- そして、そしてその第四に

## 4.4 BTRFS reported data

USB、SDカード、~~~またはフロッピードライブ~を使用している場合は、残念ながら適切なレポートデータを取得することは不可能です。

それがブレッドOSシステムドライブであると仮定すると、BTRFSファイルシステムでフォーマットされます。 BTRFSはすべてのエラーを収集し、完全なレポートを提示することができます。 BTRFSはすべてのエラーを収集し、完全なレポートを提示することができます。

- MOUNTEDである `/dev/mmcblk0p3` を仮定すると、次を実行します。

```
sudo btrfs デバイスの統計情報 /dev/mmcblk0p3
```

- 返却されます:

```
[/dev/mmcblk0p3].write_io_errs 0
[/dev/mmcblk0p3].read_io_errs 0
[/dev/mmcblk0p3].flush_io_errs 0
[/dev/mmcblk0p3].corruption_errs 0
[/dev/mmcblk0p3].generation_errs 0
```

これらの値のいずれかが非ゼロの場合、メディアは **SIGNIFICANTLY** 劣化します。

## 4.5 Should I replace the drive?

If you have just a few (<5) relocated sectors, or less than half available spare flash, reported from `smartctl` it's probably fine to keep using the disk for a little while.

しかし、スペアフラッシュを燃やしたり、数十のセクタを急速に移動させたりすることは、しかし差し迫った失敗の兆候である。

スペアフラッシュやセクタが不足すると、システムのパフォーマンスは急速に低下し、BTRFSのようなファイルシステムはロックアップされます。 書き込みの拒否ディスクの破損を拒否する


