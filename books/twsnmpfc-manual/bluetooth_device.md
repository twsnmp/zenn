---
title: "Bluetoothデバイスレポート"
---

twBlueScanセンサーで見つけたBluetoothデバイスのレポートを表示する画面の説明です。


# Bluetoothデバイスレポート画面の表示方法
メニュー「レポート」ー「デバイス」ー「Bluetooth」をクリックすれば表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_2614a38363b91c86885eab065ab27adc.png)


のような感じです。

#### ①リスト
twBlueScanからsyslogで送信されたBluetoothデバイスのリストです。信号の強度を示すRSSI、アドレス、アドレスタイプ、名前、送信元ホスト（センサーの稼働するホスト）、デバイスのベンダー、検知回数、最後に検知した日時、操作の項目があります。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_d39cc0e8efc8653ca91499a6cb6888aa.png)

左から＜詳細＞ボタン、＜削除＞ボタンです。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_e3fd6bde5f3823ae2e9a45e29fcf3503.png)

のようなダイアログにデバイスの詳しい情報を表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_a7a536436a6cf01e748707b82cfa6938.png)

のような確認ダイアログを表示します。＜削除＞ボタンをクリックすれば、対象のデバイスをレポートから削除できます。
全てのデバイスをレポートから削除したい場合はデータストア設定画面のデータクリアです。

#### ③ディスプレーフィルター
リストの内容を、アドレス、アドレスタイプ、名前、送信元ホスト、ベンダーに入力した文字列を含むものでフィルター表示できます。

#### ④＜グラフと集計＞ボタン
Bluetoothデバイスに関連したグラフのメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_e6465c1e1133e45ceaedbca28341e521.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
Bluetoothデバイスのリストを最新の情報に更新します。

# RSSI時間変化３Dグラフ

![](/images/books/twsnmpfc-manual/picture_pc_65d9e683d5a3de924c50f5a40382ed80.png)

デバイスのアドレスと検知したセンサーがX軸、日時がY軸、RSSIをZ軸にしたグラフです。名前のない一時的なアドレスのものは短い時間で削除するようにしているので通りすがりのデバイスは、離れた場所に表示されます。これは面白いです。

# RSSI位置変化３Dグラフ

![](/images/books/twsnmpfc-manual/picture_pc_bf7ae59b4ae7262596565ec6eef4ec86.png)

twBlueScanが稼働するホスト名がX軸、検知したデバイスのアドレスがY軸、RSSIをZ軸にしたグラフです。精度の同じセンサーを考えて配置すれば、デバイスの位置を特定できるかと思って作ったグラフです。センサーの精度が違うようでこのようなグラフになっています。センサーにはRaspberry Piを使うのが良いようです。

# Bluetoothデバイスレポートの情報源
twBlueScanというセンサープログラムを稼働させてTWSNMP　FCにsyslogで情報を送った場合に自動的にレポートが作成されます。twBlueScanの説明は別の記事に書きます。

