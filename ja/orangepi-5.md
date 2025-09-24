---
title: オレンジ Pi 5 シリーズ
description: このページにはOPI 5シリーズの便利なガイド/調整へのリンクが含まれています
published: true
date: 2025-09-21T09:45:58.585Z
tags: opi, opi-5
editor: markdown
dateCreated: 2024-09-20T15:17:37.567Z
---

# 1. サポートされているオレンジ Pi 5 シリーズ デバイス

| デバイス            | UEFI | サポート | 既知の問題                                      |
| --------------- | ---- | ---- | ------------------------------------------ |
| 橙色のPi 5         | はい   | はい   | Sata M.2 SSD は動作しない場合があります |
| オレンジ Pi 5B      | はい   | はい   | OPI5 イメージを使用し、wifi の DTBO が動作するように要求します。   |
| オレンジ Pi 5 Plus  | はい   | はい   |                                            |
| オレンジ Pi 5 Pro   | いいえ  | はい   |                                            |
| オレンジPi 5 Max    | いいえ  | はい   |                                            |
| オレンジ Pi 5 Ultra | いいえ  | はい   |                                            |
| オレンジ Pi CM5     | いいえ  | はい   |                                            |

> Orange Pi 5、5B および 5 Pro は RK3588S を使用しています。 一方、5 Plus と 5 Max は RK3588 を使用します (PCIe および mipi レーンが利用可能です)
> {.is-info}

### Tabset {.tabset}

#### 橙色のPi 5

> 私たちは「_opi5_」とあだ名しました。正直なところ、誰にも時間がない、忍耐力があるからです。 ばかげた長さを繰り返し言ったり入力したりしたいと思う人もいます 不必要に形式的で、穏やかに迷惑な名前 "OrangePi 5" - 特に誰もがあなたがとにかく何を意味するか正確に知っている場合。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- Rockchip RK3588S, 8-core (4×Cortex‐A76 @ ~2.4GHz + 4×Cortex‐A55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB
- ストレージ: microSD スロット; PCIを介した M.2 NVMe ; 既定の eMMC ソケットなし (SPI-flash のみ)
- ビデオ/ディスプレイ: HDMI2.1 最大8K@60Hz; USB‐C ディスプレイポート; デュアル MIPI D‐PHY 出力; マルチ
- 接続性: バージョンに応じてM.2またはモジュールを介してギガビットイーサネット、オプションのWiFi/BT、その他のポートなど。
- パワー: 5V/4A
- ~100 × 62 mmのボードサイズ。

#### オレンジ Pi 5 Plus

> 私たちは「_opi5b_」とあだ名しました。正直なところ、誰にも時間がない、忍耐力があるからです。 ばかげた長さを繰り返し言ったり入力したりしたいと思う人もいます 不必要に形式的で、穏やかに迷惑な名前 "OrangePi 5B" - 特に誰もがあなたがとにかく何を意味するか正確に知っている場合。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- Rockchip RK3588S, 8-core (4×Cortex‐A76 @ ~2.4GHz + 4×Cortex‐A55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB
- ストレージ:多くのバリエーションで32GBのeMMC、MicroSD、一部のモデルでNVMe用のM.2キースロット(または限定)はありませんか?
- ディスプレイ/ビデオ：HDMI2.1から8K@60Hzまで、USB-C経由でDisplayPort、MIPIラインなど。
- 接続性: オンボードWiFi6 + BT5.0モジュール、ギガビットイーサネットなど
- パワー: 5V/4A
- ~100 × 62 mmのボードサイズ。

#### オレンジPi 5 Max

> 私たちは「_opi5plus_」とあだ名しました。正直なところ、誰にも時間がない、忍耐力があるからです。 ばかげた長さを繰り返し言ったり入力したりしたいと思う人もいます 不必要に形式的で、穏やかに迷惑な名前 "OrangePi 5 Plus" - 特に誰もがあなたがとにかく何を意味するか正確に知っている場合。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- SoC: Rockchip RK3588 (non-S), 8-core (4×Cortex‐A76 @ ~2.4GHz + 4×Cortex‐A55 @ ~1.8GHz)
- RAM: LPDDR4/x, 4/8/16/32 GB
- ストレージ: モジュール、NVMeなどを含む
- ビデオ/ディスプレイ:高解像度、複数のHDMI / MIPIなど。
- 接続性: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0.

#### オレンジ Pi CM5

> 私たちは「_opi5pro_」とあだ名しました。正直なところ、誰にも時間がない、忍耐力があるからです。 ばかげた長さを繰り返し言ったり入力したりしたいと思う人もいます 不必要に形式的で、穏やかに迷惑な名前 "OrangePi 5 Pro" - 特に誰もがあなたがとにかく何を意味するか正確に知っている場合。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- SoC: RK3588S (8nm), 8-core (4×Cortex‐A76 @ ~2.4GHz + 4×Cortex‐A55 @ ~1.8GHz)
- RAM: LPDDR5, オプション4/8/16 GB
- ストレージ:MicroSD、eMMCソケットまたはSPIフラッシュ、NVMe/SATAなどのM.2 M-キー。
- ビデオ:デュアルHDMI(HDMI2.1およびHDMI2.0);最大8K@60Hz、MIPI DSIなどをサポートします。
- 接続性: ギガビットイーサネット; WiFi5 + BT5.0; 通常の5/5Bより小さいボード(89×56mm)。
- 電力やその他のインターフェースもシフトしました。

#### オレンジ Pi 5 Pro

> 私たちは「_opi5max_」とあだ名しました。正直言って、誰にも時間がない、忍耐力があるからです。 ばかげた長さを繰り返し言ったり入力したりしたいと思う人もいます 不必要に形式的で、穏やかに迷惑な名前 "OrangePi 5 Max" - 特に誰もがあなたがとにかく何を意味するか正確に知っている場合。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- SoC: Rockchip RK3588 (non-S), 8-core (4×Cortex‐A76 @ ~2.4GHz + 4×Cortex‐A55 @ ~1.8GHz)
- RAM: LPDDR5, オプション4/8/16 GB
- ストレージ:eMMCソケット(32‐256 GBオプション)、microSD、M.2 NVMeスロット。
- ビデオ: 2×HDMI2.1 最大8K@60Hz; MIPI DSI; など。
- 接続性: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0.
- 基板サイズ~89×57 mm。

#### オレンジ Pi 5 Ultra

> 「_opi5ultra_」とあだ名しました正直言って誰にも時間がないからです ばかげた長さを繰り返し言ったり入力したりしたいと思う人もいます 不必要に形式的で、穏やかに迷惑な名前 "OrangePi 5 Ultra" — 特に誰もがあなたがとにかく何を意味するか正確に知っている場合。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- SoC: Rockchip RK3588 (non-S), 8-core (4×Cortex‐A76 @ ~2.4GHz + 4×Cortex‐A55 @ ~1.8GHz)
- RAM: LPDDR5, オプション4/8/16 GB
- ストレージ:eMMCソケット(32‐256 GBオプション)、microSD、M.2 NVMeスロット。
- ビデオ: 2×HDMI2.1 最大8K@60Hz; MIPI DSI; など。
- 接続性: 2.5 Gbps Ethernet (RTL8125BG), WiFi6E + BT5.3/BLE; USB 3.0/2.0.
- 基板サイズ~89×57 mm。

#### オレンジ Pi 5B

> 「_opicm5_」とあだ名しました。
> {.is-info}
> {.is-info}
> {.is-info}

仕様:

- SoC: RK3588S (8nm)
- RAM: LPDDR4/4x, オプション: 2/4/8/16 GB
- ストレージ:ベース/キャリアボード上のM.2キー‐Mなどを介してオンボード(最大256GB)、microSD、拡張可能、インターフェイスに応じてSATAまたはPCIeのサポート。
- ビデオ:HDMI2.1またはeDP、MIPI DSI TXなど、8Kビデオサポート、複数のカメラインターフェース。
- 接続性: WiFi5 + BT5 (AP6256 モジュール)、USB ポートなど
- 物理的:モジュールフォームファクタ; 基板またはキャリアが必要です。 サイズは〜40×55 ミリメートルモジュール。

# 2. ダウンロード

画像のダウンロードリンクは、 [website](https://bredos.org/download.html)にあります!