---
title: BtrfsスナップショットとTimeshift
description: Timeshift スナップショットとシステムロールバックのセットアップに関する包括的なガイド
published: true
date: 2025-10-01T09:05:40.858Z
tags:
editor: markdown
dateCreated: 2024-09-27T19:19:08.209Z
---

# 1. はじめに

Btrfsファイルシステムのスナップショット機能を使用して、システムのスナップショットやロールバックを実行できます。 時間差は、このプロセスを簡単にするユーザーフレンドリーなグラフィカルアプリケーションです! 時間差は、このプロセスを簡単にするユーザーフレンドリーなグラフィカルアプリケーションです!

# 2. GRUB から grub-btrfs でタイムシフトスナップショットを起動します

適切に設定されている場合、`grub-btrfs` を使用すると、GRUBメニューから直接Timeshift スナップショットを起動でき、システムのロールバックが簡単かつ迅速に行えます。

## 2.1: grub-btrfs のインストール

- `grub-btrfs`をインストールするには:

```
sudo pacman -S grub-btrfs
```

`timeshift-autosnap` をインストールすると、パックマン経由でパッケージをアップグレードする前に、タイムシフトスナップショットが自動的に作成されます。 これにより、システムに変更が加えられる前に常に復元ポイントがあることが保証されます。

- インストールが完了すると、GRUB設定ファイルが更新されるたびに、既存のTimeshift BtrfsスナップショットのGRUBブートエントリが自動的に作成されます。 You can update the GRUB configuration with:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 2.2: GRUB設定の自動アップデート

`grub-btrfs`は、新しいTimeshift Btrfsスナップショットが作成されるたびにGRUBアップデートプロセスを自動化できます。

- Run the following command to edit the grub-btrfs path unit:

  ```
  sudo systemctl edit --full grub-btrfs.path
  ```

- Replace the content with the following:
  ```
  [Unit]
  Description=Monitors for new snapshots
  DefaultDependencies=no
  Requires=run-timeshift-backup.mount
  After=run-timeshift-backup.mount
  BindsTo=run-timeshift-backup.mount

  [Path]
  PathModified=/run/timeshift/backup/timeshift-btrfs/snapshots

  [Install]
  WantedBy=run-timeshift-backup.mount
  ```

- このステップは必要に応じて可逆的です。以下を使用します。
  ```
  sudo systemctl revert grub-btrfs.path
  ```

## 2.3: 自動GRUBアップデートを有効にする

- Activate the automatic update of the GRUB configuration file by running:

```
sudo systemctl enable --now grub-btrfs.path
```

- 設定ファイルを編集することで、grub-btrfsをさらに設定できます:

```
sudo nano /etc/default/grub-btrfs/config
```

---

# 3. Timeshift-autosnapでパッケージをアップグレードする前に自動システムスナップショットを作成する

`timeshift-autosnap` をインストールすると、パックマン経由でパッケージをアップグレードする前に、タイムシフトスナップショットが自動的に作成されます。 これにより、システムに変更が加えられる前に常に復元ポイントがあることが保証されます。 これにより、システムに変更が加えられる前に常に復元ポイントがあることが保証されます。 これにより、システムに変更が加えられる前に常に復元ポイントがあることが保証されます。

## 3.1: timeshift-autosnap のインストール

- `timeshift-autosnap` をインストールするには:

```
yay -S timeshift-autosnap
```

> `timeshift-autosnap` は、正常に動作する前にデバイスを再起動する必要があります。
> これを実行することはできません！
> {.is-warning}
> {.is-warning}
> これを実行することはできません！
> {.is-warning}
> {.is-warning}

## 3.2: GRUBの重複アップデートを防止

timeshift-autosnap によってスナップショットが作成されたときに GRUB が2回更新されないようにするには、設定ファイルを変更することをお勧めします。 Set `updateGrub` to `false` by editing the following file:

- 堅牢なスナップショットシステムを使用すると、アップデートやシステムの変更中に問題が発生した場合に備えて一日を節約できます。
  {.is-success}
  {.is-success}

```
sudo nano /etc/timeshift-autosnap.conf
```

`updateGrub=true`を`updateGrub=false`に変更します。

> 堅牢なスナップショットシステムを使用すると、アップデートやシステムの変更中に問題が発生した場合に備えて一日を節約できます。
> {.is-success}
> {.is-success}

