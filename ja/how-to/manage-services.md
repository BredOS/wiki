---
title: サービスを管理する方法
description:
published: true
date: 2025-10-05T07:04:12.252Z
tags:
editor: markdown
dateCreated: 2025-09-30T10:31:51.284Z
---

# 🔄 1. 入門情報

サービスの管理は、Linuxシステムの管理の中核となるものです。 systemd スイートの一部である systemctl は、BredOS を含むほとんどの最新のディストリビューションにおけるジョブの主要なツールです。 サービスを開始する必要があるかどうか、停止し、その状態を確認してください。 または、起動時に起動するように設定します。systemctlは一貫性のある強力なインターフェイスを提供します。 このガイドでは、システムサービスを自信を持ってコントロールするのに役立つ重要なコマンドと実践例をご紹介します。

# 📥 2. サービスを調べる

## 2.1 「bredos-news」あり

- 「bredos-news」ツールは、コマンドラインを開くたびに自動的に開始されます。

![bredos-news.png](/systemd/bredos-news.png)

出力の最後に「システムは正常に動作しています」というテキストが表示されます。 これは、ブート時に起動するはずのすべてのサービスがエラーなしで開始されたことを意味します。 端末を起動したばかりの場合、「**X** サービスレポートの状態を有効にする」という警告が表示されることがあります。 多くのサービスが並行して開始でき、開始時の遅延につながる可能性があります。 この警告は数分後に消えるはずです。

エラーメッセージが表示された場合、"**X** サービスのレポートステータスが失敗しました" 1つ以上のサービスの起動に失敗しました。

## 2.2 `systemctl`で

- コンピュータ上のすべてのシステム全体のサービスを一覧表示するには、次を実行します。

```
systemctl list-units --type=service
```

- ユーザー全体のすべてのサービスをコンピュータに表示するには、次を実行します。

```
systemctl list-units --type=service --user
```

これはサービスのリストを出力します。 矢印キーで移動するか、 <kbd>スペース</kbd> を使用して1ページ下に移動します。 <kbd>Q</kbd> キーで終了します。

サービスは、行「SUB」に示すように異なる状態を持つことができます。 `running`、`exited`、または `failed`のいずれかです。

- `running`サービスはバックグラウンドタスクを実行します。 その良い例がネットワークマネージャです。 このサービスはネットワーク接続を管理します。 イーサネットケーブルを常に差し込むことができるため、プログラムはネットワークを適切に管理するために連続的に実行する必要があります。 これは `running` サービスによって実現されます。

- `exited` サービスは、起動時に実行され、タスクを実行し、その後きれいに終了します。 この良い例として、systemd-tmpfiles-setup サービスがあります。 起動時に起動し、ramdisk をセットアップし、/tmpにマウントし、そして優雅に終了します。

- `failed` サービスが正しく起動しなかったか、エラーコードで実行中に問題が発生して停止しました。 これは、システムが壊れていることを意味するものではありませんが、それを修正することはまだお勧めできます。

与えられたサービスの状態をチェックすることもできます。これは、失敗した場合にエラーメッセージを含む、より多くの出力を提供します。

- 指定されたサービスのステータスを確認するには:

```
systemctl 状態 <your service name here>
```

- 例えば、以下に問題を含む失敗したサービスの出力を示します。

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

上記の例では、nordvpnd サービスはライブラリの libxml2.so がないため起動に失敗しました。 この情報を使用すると、それは簡単に修正可能です。

# 4. サービスの管理

サービスは手動または起動時または起動時に開始および/または停止することができます。 サービスの動作を管理するには、以下を行います。

- サービスを手動で開始するには、次を実行します。

```
sudo systemctl start <your service name here>
```

- そして、それを停止するには、次を実行します。

```
sudo systemctl stop <your service name here>
```

このロジックは、起動時にサービスを有効化および無効化し続けます。 `systemctl enable` を使用すると起動時に起動できます。systemctl disable`を使用すると起動時に起動できなくなります。 パラメータ`--now\` を使用すると、起動して同時に有効にすることができます。

- たとえば、起動時に nordvpnd を有効にして同じコマンドで開始したい場合は、以下を実行します。

```
sudo systemctl enable --now nordvpnd
```

# 🚀 4. サービスの編集と作成

また、好みのサービスを編集または作成することもできます。 システム全体のサービスファイルは通常、 `/usr/lib/systemd/system` または `/etc/systemd/system` に保存され、ユーザ全体のサービスファイルは `~/.config/systemd/user` または `/etc/systemd/user` に保存されます。

- システム全体の service-file を作成するには、以下を実行します。

```
sudo nano /etc/systemd/system/<your service-file name here>.service
```

- 次に、新しく作成したファイルにいくつかの情報を入力します。 例:

```
[Unit]
Description=Run my one-shot script at start
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/my-oneshot script.sh
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```

このservice-file は /usr/local/bin/my-oneshot-script.sh を実行し、スクリプトがきれいに終了した後に `exited` と入力します。

- 既存のサービスを編集するには、次を実行します。

```
sudo systemctl 編集 <your service-file name here>
```

> service-files の編集は **危険**であることに注意してください!
> {.is-danger}

- service-fileを編集した後、syystemd-daemonをリロードする必要があります:

```
sudo systemctl daemon-reload
```

# 🔄 3. チートシート

多くのLinuxの気晴らしは、システムのためのチートシートを公開します。 基本的には全部同じなので、[システム用レッドハットのチートシート](https://access.redhat.com/sites/default/files/attachments/12052018_systemd_6.pdf)へのリンクを提供します。
