---
title: RK3588でUEFIをアップデートする方法
description: BredOSを実行しているRK3588ベースのデバイスでUEFIファームウェアをアップデートする方法を学ぶ
published: true
date: 2025-02-23T15:28:48.131Z
tags: null
editor: markdown
dateCreated: 2025-02-23T15:28:48.131Z
---

# 🔄 RK3588 デバイスで UEFI を更新します

RK3588ベースのデバイス用UEFIファームウェアは、パッケージマネージャを介してインストールできます。 特定のデバイスの正しいパッケージを見つけるには、以下を実行してください:

```
sudo pacman -Ss uefi
```

利用可能なすべての UEFI ファームウェアパッケージが一覧表示されます。 リストからデバイスの正しいパッケージを特定します。 例:

- **エッジ2:** `edge2-uefi`
- **Fydetab Duoの場合:** `fydetab-duo-uefi`
- **オレンジ Pi 5:** `orangepi-5-uefi`
- **Rock 5Bの場合:** `rock-5b-uefi`
- \*(出力に記載されているその他) \*

---

## 📥 ファームウェアのインストール

デバイスの正しいパッケージを特定したら、以下を使用してインストールしてください:

```
sudo pacman -S <device-uefi-package>
```

例えば、**Fydetab Duo**を使用している場合は、以下を実行します。

```
sudo pacman -S fydetab-duo-uefi
```

---

## 🛠️ UEFI ファームウェアのフラッシュ

インストール後、ファームウェア画像は `/usr/share/edk2/<device-name> /` に保存されます。 システムはファームウェアをフラッシュするための特定のコマンドを提供します。\
コマンドの一般的な形式は次のとおりです。

```
sudo dd if=/usr/share/edk2/<device-name>/<device-name>_UEFI_Release_vX.XX.X.img of=/dev/<TARGET_DEVICE> bs=512 skip=64 seek=64 conv=notrunc
```

`<TARGET_DEVICE>` を適切なストレージデバイスに置き換えます:

- **eMMC** 用 `/dev/mmcblk0`
- `/dev/mmcblk1` for **SD card**
- `/dev/mtdblock0` for \*\*SPIフラッシュ

たとえば、**Fydetab Duo**で **eMMCストレージ**を使用している場合、コマンドは次のようになります。

```
sudo dd if=/usr/share/edk2/fydetab-duo/fydetab-duo_UEFI_Release_v0.12.3.img of=/dev/mmcblk0 bs=512 skip=64 seek=64 conv=notrunc
```

---

✅ **完了！** デバイスの UEFI ファームウェアが更新されました。 🚀
