---
title: ホームページ
description: 
published: true
date: 2024-09-21T12:45:24.603Z
tags: 
editor: markdown
dateCreated: 2024-09-21T12:32:53.311Z
---

# 🍞 BredOS Wiki

## 🌟 概要

BredOS のドキュメントへようこそ！ BredOSは、ARMベースのシングルボードコンピュータ(SBC)用に特別に設計された、ユーザーフレンドリーなArchベースのLinuxディストリビューションです。
このドキュメントでは、BredOS のインストール、設定、および使用方法について説明します。

![](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/raw/main/Images/Linux/BredOS/preview.jpg)

## 📚 目次

1. [🔍 はじめに](#はじめに)
2. [🚀 機能](#機能)
3. [🛠️ システム要件](#system-requirements)
4. [💽 インストール](/installation)
5. [📦 パッケージ管理](#パッケージ管理)
6. [🐞 トラブルシューティング](#トラブルシューティング)
7. [❓FAQ](#faq)
8. [🌐 コミュニティとサポート](#コミュニティとサポート)
9. [🤝 Contributing](#contributing)

## 🔍 はじめに

BredOSは、ARMベースのシングルボードコンピュータのユーザーにシームレスで使いやすい体験を提供することを目指しています。 Arch Linuxのパワーと柔軟性を活用する ブレッドOSは、幅広いユースケースに合わせてカスタマイズ可能な堅牢なプラットフォームを提供します。

## 🚀 機能

- **🖥️ ユーザーフレンドリーなインターフェイス**: ナビゲーションと使用を簡単にするための簡単で直感的なユーザーインターフェイス。
- **🎯 Arch-Based**: Arch-Based\*\*: ArchのLinux上に構築されており、パッケージとローリングリリースモデルの広大なリポジトリへのアクセスを保証します。
- **🔧 ARM Support**: ARMベースのシングルボードコンピュータに最適化されているため、Rock 5Bなどのデバイスに最適です。
- **⚡ Lightweight**: 最小の膨張、軽量で応答性の高いシステムを確保します。

## 🛠️ システム要件

- **🖥️ サポートされているデバイス**:
  - Radxa Rock 5 A/B/B+/C/D
  - Radxa Rock 4 C+
  - Radxa NX5キット
  - IndieDroid Nova
  - オレンジ Pi 5/5B/5+
  - Khadas Edge 2
  - Khadas VIM 4
  - クールなPi 4B
  - [Fydetab Duo](https://github.com/LinuxDroidMaster/Fydetab-Duo-DroidMaster-wiki/blob/main/Documentation/Linux_distros/bredos.md)
- **🧠 最小RAM**: 2 GB
- **💾 ストレージ**: 16 GB microSD カード以上
- **🌐 Network**: Optional

## 💽 インストール

詳細はformat@@0(/installation) のページをご覧ください。

## 📦パッケージ管理

BredOS は Arch Linux のパッケージマネージャである `pacman` を使用します。 以下に共通のコマンドを示します。

- 🔄 パッケージ一覧を更新: `sudo pacman -Syu`
- ➕ Install a package: `sudo pacman -S [package_name]`
- ➖ パッケージを削除: `sudo pacman -R [package_name]`
- 🔍 パッケージを検索: `pacman -Ss [package_name]`

## :lady_betle: トラブルシューティング

BredOS で問題が発生した場合は、 [discord](https://discord.gg/jwhxuyKXaa) に参加してください。

## ❓ FAQ

### ❓ Q: BredOS でサポートされているデバイスは何ですか？

A: BredOS は、さまざまな ARM ベースのシングルボードコンピュータをサポートしており、format@@0(#system-requirements) で完全なリストをご利用いただけます。

### 🔄 Q: BredOS をアップデートするには?

A: `sudo pacman -Syu`コマンドを使って、 `pacman` パッケージマネージャを使ってブレッドOSをアップデートできます。

### 📦 Q: 追加のソフトウェアパッケージはどこで見つけることができますか?

A: Arch User Repository(AUR)で追加のソフトウェアパッケージを見つけて、`yay`または`paru`を使用してインストールできます。

## 🌐 コミュニティとサポート

BredOS コミュニティに参加して、サポートを受けたり、アイデアを共有したり、プロジェクトに貢献したりしましょう。

- [📱 Telegram](https://t.me/bredoslinux)
- [💬 Discord](https://discord.gg/jwhxuyKXaa)
- [💻 GitHub](http://github.com/BredOS)

## 🤝 Contributing

BredOSはオープンソースのプロジェクトであり、貢献は歓迎です! 以下の方法で貢献できます：

- 🐛 バグと課題を報告
- 💻 パッチと改善点を提出する
- 📄 ドキュメントの書き込みと改善
- 🧑‍🤝‍🧑 コミュニティフォーラムやチャットで他のユーザーを助けます

貢献の詳細については、[💻 GitHub](http://github.com/BredOS)をご覧ください。または[💬 Discord](https://discord.gg/jwhxuyKXaa)または[📱 Telegram](https://t.me/bredoslinux)に参加してください。
