---
title: "センサー"
---


TWSNMP FCに情報を送信してくるセンサーのリストを表示する画面についての説明です。


# センサーリスト画面の表示方法
メニューの「センサー」をクリックすると表示できます。

# センサーリスト画面の構成

![](/images/books/twlogaian-manual/picture_pc_d7e61783ed064b76ab858f1d32b2592c.png)

#### ①センサーリスト
センサーの状態、送信元、種別などのリストです。項目をクリックすると並べ替えできます。状態は、データ送信が行われなくなってからの時間で悪化するようになっています。一定期間、通信してこない場合に異常と判断するという意味です。

#### ②フィルター
送信元のホスト名と種別でフィルタ表示できます。

#### ③操作ボタン

![](/images/books/twlogaian-manual/picture_pc_7b3511453cc38bf43d6f5e40f892cf98.png)

左から＜詳細表示＞＜削除＞のボタンです。
＜削除＞ボタンをクリックすると

![](/images/books/twlogaian-manual/picture_pc_11c46676ea9414b392a12956a5e779c6.png)

の確認ダイアログが表示されます。

### ④CSVボタン
センサーリストをCSVファイルに保存します。

#### ⑤EXCELボタン
センサーリストをEXCELファイルに保存します。

#### ⑥更新ボタン
センサーリストを最新の標示に更新します。

# センサー情報画面
センサーリストの操作から＜詳細＞（目のアイコン）をクリックすると

![](/images/books/twlogaian-manual/picture_pc_11c46676ea9414b392a12956a5e779c6.png)

のようなセンサーに関する情報画面が標示されます。＜グラフ標示＞をクリックするとサブメニューが表示されます。NetFlowとIPFIXのセンサーは各種グラフには対応していません。以下のグラフはTWSNMPシリーズのセンサーのみ表示できます。

# 統計情報グラフ
センサーからのデータ送信量に関するグラフです。

![](/images/books/twlogaian-manual/picture_pc_df3dc11c6d04331f00c756c3d30403fa.png)

# CPU/Memoryグラフ
センサーが稼働する環境のCPUとメモリー使用量のグラフです。

![](/images/books/twlogaian-manual/picture_pc_98a9899b8b2c849b1431175dfd28bf6e.png)

# 通信量グラフ
センサーが稼働する環境の通信量に関するグラフです。

![](/images/books/twlogaian-manual/picture_pc_45533aa9a1413b7c976146a9cebc04af.png)

プロセスと負荷グラフ
センサーが稼働する環境のプロセス数とLoad　Avg.のグラフです。

![](/images/books/twlogaian-manual/picture_pc_ea8d0f69b8c8512248a8c869a2b40a6e.png)

# センサープログラムについて



TWSNMP FCのレポート作成を助けてくれるセンサープログラムの説明です。センサーはサッカーチームのファワードのように前線で働くプログラムです。集めた情報を司令塔であるTWSNMP FCにNetFlowやsyslogなどの標準的なプロトコルで送信します。

センサーの全体図は

![](/images/books/twlogaian-manual/picture_pc_e1f75e181aec3f7f5a7f3f11112b43ee.png)

です。

#### softflowd(NetFlow/IPFIXセンサー）
Linuxのパソコン環境でパケットキャプチャーしてNetFlow/IPFIXの情報を送信するためのプログラムです。Linuxのディストリビューションにはパッケージとして組み込まれています。インストールすれば使えます。
TWSNMP FCのためにDocker版を作って公開しています。
https://hub.docker.com/repository/docker/twsnmp/softflowd


```shell
docker run --net host -d --rm twsnmp/softflowd -i enp3s0f0 -v 10 -n 127.0.0.1:2055
```

のように起動すれば使えます。 enp3s0f0がネットワークインターフェイスの名前です、 -v 10にすればIPFIXで送信します。 -n 127.0.0.1:2055が宛先です。
TWSNMP FCへ送信する場合はポート番号を2055にしてください。
このセンサーのデータをTWSNMP FCで受信するとNetFlow分析のレポートを表示できます。

#### twpcap(パッケットキャプチャーセンサー）
パケットキャプチャーからTWSNMP FCでレポートを作成するために必要な情報をsyslogで送信するためのセンサープログラムです。以下の情報を取得できます。

- モニタしたパケット数の統計情報
- ネットワーク上のEthernetパケットの種類別集計
- IPアドレスとMACアドレスの関係(ARP,IPv4,IPv6)
- DHCPサーバーとクライアントの情報
- DNSサーバーとクライアントの問い合わせ情報
- NTPサーバーの情報
- RADUISサーバーとクライアントの情報
- サーバーとクライアントのTLS通信の情報（TLSバージョン、暗号方式）
このセンサープログラムは、TWSNMP FCのWindows,Mac OS,Linuxパッケージに含まれています。パッケージをインストールすれば使えます。Docker版も公開しています。

https://hub.docker.com/repository/docker/twsnmp/softflowd


基本的な使用方法は

1. キャプチャできるネットワークインターフェイスを調べる

```
>'C:\Program Files\TWSNMP FC\twpcap.exe' -list
```

2. twpcapを起動する

```
>'C:\Program Files\TWSNMP FC\twpcap.exe' -iface "<調べたインタ-フェイス名>" -syslog <syslogの送信先>
```

で起動できます。

コマンドのパラメータは
```
Usage of C:\Program Files\TWSNMP FC\twpcap.exe:
 -cpuprofile file
   	write cpu profile to file
 -iface string
   	monitor interface
 -interval int
   	syslog send interval(sec) (default 600)
 -list
   	list interface
 -memprofile file
   	write memory profile to file
 -retention int
   	data retention time(sec) (default 3600)
 -syslog string
   	syslog destnation list
```

です。プログラムの詳しい説明は、

https://github.com/twsnmp/twpcap


にあります。

#### twWifiScan（無線LANアクセスポイントセンサー）

無線LANのアクセスポイントに関するレポートをTWSNMP FCで作成するために必要な情報をsyslogで送信するためのセンサープログラムです。 以下の情報を取得できます。

- モニタしたパケット数の統計情報
- センサーのリソース
- アクセスポイントのBSSID
- アクセスポイントのSSID
- アクセスポイントのRSSI
- アクセスポイントの利用チャネル
- アクセスポイントの暗号化の有無

このセンサーはTWSNMP FCのWindows,Mac OS,Linuxパッケージに含まれています。

```
>'C:\Program Files\TWSNMP FC\twWifiScan.exe' -syslog ＜syslogの送信先>
```

のように起動できます。

起動パラメータは以下です。

```
>'C:\Program Files\TWSNMP FC\twWifiScan.exe' -h
Usage of C:\Program Files\TWSNMP FC\twWifiScan.exe:
 -cpuprofile file
   	write cpu profile to file
 -iface string
   	monitor interface (default "wlan0")
 -interval int
   	syslog send interval(sec) (default 600)
 -memprofile file
   	write memory profile to file
 -syslog string
   	syslog destnation list
```

プログラムの詳しい説明は、

https://github.com/twsnmp/twWifiScan

にあります。

#### twBlueScan(Bluetoothデバイスセンサー）
Linuxマシンで周辺にあるBlueToothデバイスの情報を収集してsyslogで送信するためのセンサー プログラムです。

収集できる情報は

- デバイスのアドレス
- アドレスの種類(randam/public)
- 名前
- RSSI(信号の強度)
- 製造元メーカー
- オムロンの環境センサーの情報
- SwitchBotの温度、湿度センサーの情報

です。
このセンサーはLinux版のTWSNMP FCのみに含まれています。

```
#./twBlueScan -adapter hci0 -syslog 192.168.1.1
```

のように起動します。 192.168.1.1が送信先のTWSNMP FCのアドレスです。
起動パラメータは、

```
#twBlueScan -h
Usage of /tmp/twBlueScan:
 -active
   	active scan mode
 -adapter string
   	monitor bluetooth adapter (default "hci0")
 -addr string
   	make address to vendor map
 -code string
   	make company code to vendor map
 -cpuprofile file
   	write cpu profile to file
 -debug
   	debug mode
 -interval int
   	syslog send interval(sec) (default 600)
 -memprofile file
   	write memory profile to file
 -syslog string
   	syslog destnation list
```

です。Bluetoothが動作しない環境では動作しません。
プログラムの詳しい説明は、

https://github.com/twsnmp/twBlueScan

にあります。

# twWinlog(Windowsイベントログセンサー）
Windowsのイベントログの情報を集計してsyslogで送信するセンサープログラムです。以下の情報を取得できます。

- イベント数の集計
- イベントID別の集計
- ログオンに関する情報(4624, 4625, 4648, 4634, 4647)
- アカウントの変更に関する情報　　　　　(4720,4722,4723,4724,4725,4726,4738,4740,4767,4781)
- 特権アクセスに関する情報(4672,4673)
- Kerberos認証に関する情報(4768,4769)
- スケジュールタスクに関する情報(4698)
- プロセスの起動、停止に関する情報(4688, 4689)
- ログオン失敗の通知(4625)
- Kerberosチケット要求失敗の通知(4768,4769)
- イベントログ消去の通知(1102)

このセンサーは、Windows版のTWSNMP FCのパッケージにのみ含まれます。
インストールしたWindows PCのイベントログを送信する場合は

```
>'C:\Program Files\TWSNMP FC\twWinlog.exe'  -syslog 192.168.1.1
```

のように起動します。
他のWindows PCのイベントログを送信する場合は、

```
>'C:\Program Files\TWSNMP FC\twWinlog.exe' -syslog 192.168.1.1 -remote <PCのアドレス> -user <ユーザー名> -password <パスワード>
```

のように起動すればよいです。リモートのWindow PCにイベントログの収集を許可する設定が必要です。

https://help.sumologic.jp/03Send-Data/Sources/01Sources-for-Installed-Collectors/Remote-Windows-Event-Log-Source/Preconfigure-a-Machine-to-Collect-Remote-Windows-Events

とかです。

# パケットキャプチャーするセンサーのための環境

NetFlowに対応したネットワーク機器は高価なので、安上がりに対応するには、古いPCを再利用したりminiPC

https://www.amazon.co.jp/gp/bestsellers/computers/6111451051

にLinuxとDockerをインスールするのがお勧めです。RaspBerry Piでもよいかもしれませんが処理能力的に心配ではあります。
パッケットキャプチャーするためには、ポートミラーリングに対応したスイッチングHUBがあればよいです。今、探したらSNMP対応で６０００円になっていました。SNMPなしならもっと安いものがあります。

https://www.amazon.co.jp/dp/B01N32P5QZ?tag=note0e2a-22&linkCode=ogi&th=1&psc=1

これらを、

![](/images/books/twlogaian-manual/picture_pc_0eeed457cde35cea3c16232a26a5efcc.png)

のようにすればよいです。私の環境だと10000円ぐらいでモニタできています。


