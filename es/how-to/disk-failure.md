---
title: Discos de error de Manejo
description: Una guía sobre los datos de S.M.A.R.T y la sustitución de discos
published: true
date: 2025-06-01T10:33:55.798Z
tags:
editor: markdown
dateCreated: 2025-06-01T10:33:55.798Z
---

# DECLARACIÓN IMPORTANTE

Esta guía es un conjunto de consejos recopilados a partir de experiencias personales.
Asegurar la comprensión y el riesgo adecuados al ejecutar cualquier comando de esta guía.
La pérdida de datos es posible.

# Fallos reportados

El servicio BredOS News informará ahora sobre unidades dañadas o defectuosas que estén adjuntas y que presenten los datos de S.M.A.R.T.

Si ha sido vinculado a esto desde BredOS News, diríjase a la siguiente sección.

Fallos

# Viendo los datos de S.M.A.R.T (HDD)

Asumiendo el disco duro `/dev/sda`, para ver sus datos S.M.A.R.T, ejecutar:

```
sudo smartctl -a /dev/sda
```

Esto imprimirá un informe grande:

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

De todo esto, los siguientes datos son importantes para buscar:

- `SMART overall-health self-assessment`, que debe ser "PASSED". Si se informa de cualquier otro valor, la unidad debe ser reemplazada con prise.
- `Reallocated_Sector_Ct`, el número de sectores reubicados, que si es más de uno solo indica un riesgo significativo de fallo en cascada.

# Viendo datos de S.M.A.R.T (NVME)

Asumiendo NVME `/dev/nvme0`, para ver sus datos S.M.A.R.T, ejecutar:

```
sudo smartctl -a /dev/nvme0
```

Asumiendo que la NVME soporta S.M.A.R.T, esto imprimirá un pequeño informe:

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

Aquí, los únicos valores importantes son:

- `Porcentaje utilizado`, que es el porcentaje de bloques de recambio usados. No debería exceder el `umbral de comparación disponible`, ya que este normalmente es el punto de no retorno de la unidad.
  La tasa de fallo de bloque normalmente aumentará exponencialmente pasado ese punto, lo que conducirá a un fallo total.
  Las unidades NVME son propensas a bloquear y girar Read-Only una vez que el flash de repuesto está exausto.
- `Media and Data Integrity Errors`, que indican una significativa gradación del flash.
- `Entradas de registro de información de errores`, que generalmente indican cuántas regiones de flash han sido enmascaradas con la flash.

# ¿Debo reemplazar la unidad?

Si tienes sólo unos pocos sectores (<5) reubicados, probablemente esté bien seguir usando el disco durante un tiempo.
También es correcto usar algunos bloques de flash nvme de sobra.

Sin embargo, quemar a través del flash libre o trasladar rápidamente docenas de sectores es sin embargo una señal de un fracaso inminente.

A medida que se acabe el flash libre o los sectores, el rendimiento del sistema se degradará rápidamente y los sistemas de archivos como BTRFS se bloquearán, negándose a realizar escrituras, negándose a corromper el disco.