---
title: Sata ファームウェアの修正
description:
published: true
date: 2025-09-19T05:01:28.982Z
tags:
editor: markdown
dateCreated: 2025-09-12T09:18:06.486Z
---

# 1. 前提条件

- CH341Aベースのフラッシャー
- はんだ付けの鉄またはSPIクリップのいずれか
- 新しいファームウェアファイル ( [here](/wiki-itx3588j-pics/satafw/sata_adapter_en25f40.bin)) からダウンロードします。
- Linuxがインストールされている別のデバイス（Windowsも動作するはずですが、ここではカバーされていません）

https://www.aliexpress.com/item/32263275388.html
![spi-flasher.png](/wiki-itx3588j-pics/spi-flasher.png)

> リンクの有効期限が切れた場合は、DiscordまたはTelegramからお気軽にご連絡ください。

# 2. SPIに接続

> _電源に接続する前に、すべてのコネクタが正しく配置されていることを確認してください！_
> {.is-warning}

SPIチップに接続する最も簡単な方法は、クリップを使用することです。 しっかり接続するのは少し難しいことですが、はんだ付けのスキルやツールは必要ありません。 さらに、クリップを使用すると、ボードに損傷を与える可能性は非常に低いです。 しっかり接続するのは少し難しいことですが、はんだ付けのスキルやツールは必要ありません。 さらに、クリップを使用すると、ボードに損傷を与える可能性は非常に低いです。

一方、はんだ付けの経験がある場合は、SPIチップの8つの端子を分解し、再装着することは難しい作業ではありません。

- SPIチップは、mSATAスロットのすぐ隣にSATAポートの近くにあります。 SPIチップは、mSATAスロットのすぐ隣にSATAポートの近くにあります。 「JMB575」というラベルの正方形チップを探してください。これがSATAコントローラです。 その隣には、SPIチップである「W25X40CL」というラベルの付いた小さな8ピンチップがあります。 SPIチップ上のラベルは読みにくい場合があります しかし、SATAコントローラを見つけたら、SPIチップを簡単に識別できるはずです。
  ![sata-controller-text-scaled.jpg](/wiki-itx3588j-pics/sata-controller-text-scaled.jpg) その隣には、SPIチップである「W25X40CL」というラベルの付いた小さな8ピンチップがあります。 SPIチップ上のラベルは読みにくい場合があります しかし、SATAコントローラを見つけたら、SPIチップを簡単に識別できるはずです。

![sata-controller-text-scaled.jpg](/wiki-itx3588j-pics/sata-controller-text-scaled.jpg)

## 2.1 クリップを接続する

クリップのピン1はケーブル上で色分けされています — 赤いワイヤーはそれを示します。 赤いワイヤーは、SATAポートがあるボードの端に面する必要があります。

- クリップが完全に挿入されていることを確認します。 正しく接続されている場合は、クリップを使用してボードを持ち上げることができます。

![spi-clip-connected-cut.jpg](/wiki-itx3588j-pics/spi-clip-connected-cut.jpg)

- ケーブルのもう一方の端をフラッシャーに接続します。 正しい方向は以下のとおりです。フラッシャーの USB コネクタがあなたを指している場合。 ケーブルは下の4つの穴に入って左上に赤い線が入ってるはずだ

![flasher-clip-connected-cut-scaled.jpg](/wiki-itx3588j-pics/flasher-clip-connected-cut-scaled.jpg)

## 2.2 またはSPIチップを元に戻す

はんだ付けウィックとフラックスをつかみ、鉄を加熱し、チップを半田付けします。 あなたは自分が何をしているのか知っておくべきです！ あなたは自分が何をしているのか知っておくべきです！

チップをフラッシャーに直接半田付けすることができます（これにはフラッシャーの背面にパッドがあります） または、上記のパックに含まれているアダプターボードのいずれかを使用してください。
パックの一部として、無人のボードとZIF Socketがある必要があります。 賢明に選びなさい。
パックの一部として、無人のボードとZIF Socketがある必要があります。 賢明に選びなさい。

- ピン1はチップ上に小さなドットでマークされ、フラッシャーまたはアダプターボード上に「1」と表示されます。
  ![zif-socket-cut-scaled.jpg](/wiki-itx3588j-pics/zif-socket-cut-scaled.jpg)
  または
  ![spi-soldered-cut.jpg](/wiki-itx3588j-pics/spi-soldered-cut.jpg)

![zif-socket-cut-scaled.jpg](/wiki-itx3588j-pics/zif-socket-cut-scaled.jpg)

- または

![spi-soldered-cut.jpg](/wiki-itx3588j-pics/spi-soldered-cut.jpg)

## 2.3 接続の確認

- まず、flashromをインストールする必要があります。

```
sudo pacman -S flashrom
```

> フラッシャーが3.3ボルトに設定されていることを確認してください！
> {.is-warning}

すべてのケーブルを確認し、クリップを使用している場合は、ITX-3588Jボードが電源から切断されていることを確認してください。
次に、フラッシャーをLinuxデバイスに接続し、次のコマンドを実行します。
上記のSPIチップ名が報告されている場合は、準備が整います。
次に、フラッシャーをLinuxデバイスに接続し、次のコマンドを実行します。

- 上記のSPIチップ名が報告されている場合は、準備が整います。

```
sudo flash -p ch341a_spi --flash-name
```

```
flashrom 1.4.0-devel (git:v1.2-1355-g9ccbf1cf) on Linux 6.15.7-1-BredOS (x86_64)
flashrom is free software, get the source code at https://flashrom.org

Using clock_gettime for delay loops (clk_id: 1, resolution: 1ns).
Found Winbond flash chip "W25X40" (512 kB, SPI) on ch341a_spi.
```

そうでない場合は、クリップの接続を確認したり、はんだ付け作業を確認して、すべてのコネクタの向きを確認します。

# 3. ファームウェアをフラッシュする

## 3.1 古いファームウェアのバックアップ

新しいROMを点滅させる前に、既存のROMをバックアップすることをお勧めします。
何か問題が発生した場合は、このバックアップを使用して復元できます。
何か問題が発生した場合は、このバックアップを使用して復元できます。

- 次のコマンドでフラッシュをダンプします。

```
sudo flash -p ch341a_spi -r firmware_dump.bin
```

- 次に、それをダンプし、データが正しく転送されたことを確認するために、2つのファイルを比較します。

```
sudo flash -p ch341a_spi -r firmware_dump-1.bin
diff firmware_dump.bin firmware_dump-1.bin
```

"diff" が出力を生成しない場合は、出力します。
その場合は、クリップの接続を確認するか、はんだ付け作業を確認し、すべてのコネクタの向きを確認します。
その場合は、クリップの接続を確認するか、はんだ付け作業を確認し、すべてのコネクタの向きを確認します。

## 3.2 新しいファームウェアのフラッシュ

- タイトルが示すように簡単です:

```
sudo flash -p ch341a_spi -w sata_adapter_EN25F40.bin 
```

```
flashrom 1.4.0-devel (git:v1.2-1355-g9ccbf1cf) on Linux 6.15.7-1-BredOS (x86_64)
flashrom is free software, get the source code at https://flashrom.org

Using clock_gettime for delay loops (clk_id: 1, resolution: 1ns).
Found Winbond flash chip "W25X40" (512 kB, SPI) on ch341a_spi.
===
This flash part has status UNTESTED for operations: WP
The test status of this chip may have been updated in the latest development
version of flashrom. If you are running the latest development version,
please email a report to flashrom@flashrom.org if any of the above operations
work correctly for you with this flash chip. Please include the flashrom log
file for all operations you tested (see the man page for details), and mention
which mainboard or programmer you tested in the subject line.
Thanks for your help!
Reading old flash chip contents... done.
Erase/write done from 0 to 7ffff
Verifying flash... VERIFIED.
```

"VERIFIED"という文字が表示された場合は、ファームウェアが正しく書き込まれています。 クリップを使用した場合は、単にそれを取り外してください。 あなたがチップを分解した場合、あなたは何をすべきか知っています。

> すべてのSATAポートは今正常に動作するはずです!
> {.is-success}
