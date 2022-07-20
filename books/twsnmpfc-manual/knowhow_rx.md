---
title: "syslog/SNMP TRAP/NetFlowの受信ができない時"
---

TWSNMP FCでsyslog/SNMP TRAP/NetFlowの受信ができない場合があります。その場合の対応方法についての説明です。


# 受信設定の確認
まずは、基本的な話ですがマップ設定で受信の設定がオンになっているか確認します。「何をバカな」と思うかもしれませんが忘れていることもよくあるものです。

![](/images/books/twsnmpfc-manual/picture_pc_0c86a50946a8350febc2e44635d64ed0.png)

初期設定はオフなので受信しません。

# UDPのポートが受信状態か確認する
受信する設定になっていれば対応するポートが受信状態になっています。これは、コマンドプロンプトを表示して

```
netstat -ap udp
```

というコマンドを実行すれば確認できます。Macの場合は、

```
netstat -anp udp
```

の方がポート番号が数値になるので確認しやすいです。

![](/images/books/twsnmpfc-manual/picture_pc_f4b9d03d0ad033b923b32a50b53b3398.png)

それぞれ

```
SNMP Trap:162
syslog : 514
Netflow: 2055
````

のUDPポートがリストに表示されれば受信できる状態です。ほとんど場合は、ここまでは問題ないと思います。問題なのは、次に説明するファイヤーフォールの設定です。

# ファイヤーフォールを確認する
WindowsやMacにはファイヤーフォールが搭載されています。この機能が有効な場合はファイヤーフォールによってTWSNMP FC宛のパケットがブロックされて受信できない場合があります。ファイヤーフォールの設定は、Windowsの場合、

https://pc-karuma.net/windows-10-firewall-enable-disable/

や

https://pc-karuma.net/windows-10-firewall-app-allow-communicate/

が参考なると思います。

![](/images/books/twsnmpfc-manual/picture_pc_023899d6756cb9ea48bb1300729d70f3.png)

のようにTWSNMP FCの通信が許可されていることを確認します。
（画面ではtwsnmpになっていますが、twsnmpfcと読み替えてください。）

![](/images/books/twsnmpfc-manual/picture_pc_41a97c743fade75e6abec650501c8939.png)

Macの場合は、

https://support.apple.com/ja-jp/guide/mac-help/mh11783/mac

にファイヤーフォールの設定に関する説明があります。

TWSNMP FCでsyslogなどを受信する設定にすると

![](/images/books/twsnmpfc-manual/picture_pc_025291f51751245b8f9695552fb5107b.png)

のようなダイアログが表示されます。＜許可＞をクリックすれば、TWSNMPが通信できるようになります。許可されていることは「システム設定」ー「セキュリティーとプライバシー」のファイヤーフォールタブで

![](/images/books/twsnmpfc-manual/picture_pc_815e948f0ca403e8f14c7dd6cb30c79b.png)

で確認できます。この画面から手動で追加することもできます。

# 参考のサイト
パソコンに搭載されているファイヤーフォールは、パーソナルファイヤーフォールと言われています。この言葉で検索すれば、参考になるサイトが見つかります。

https://www.techdevicetv.com/ch_windows10/17/

などが参考になるかと思います。

