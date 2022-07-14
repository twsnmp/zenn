---
title: "環境センサーレポート"
---

twBlueScan経由でBluetoothの環境センサーの情報を表示するレポートの説明です。2021年10月時点で対応している環境センサーは、オムロンとSwitchBotの温度・湿度センサーです。サーバールームや事務所の環境をモニターするために使えるかと思って作った機能です。


# 環境センサーレポート画面の表示方法
メニューの「レポート」ー「デバイス分析」ー「環境センサー」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_4e083624378fbe15a67b4409129b6536.png)

# 環境センサーレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_37a0d2d356c935afd0202c89ceda2116.png)

のような感じです。

#### ①リスト
環境センサーのリストです。信号レベル（RSSI)、アドレス、名前、受信ホスト、保持しているデータ数、測定回数、最終データの日時、操作ボタンがあります。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_97dbe30b2b6a11c2e319abde8144fda3.png)

左から＜詳細＞ボタン、＜削除＞ボタンです。
＜詳細＞ボタンをクリックすると、

![](/images/books/twsnmpfc-manual/picture_pc_2edc160b53f9a5524d6865f4c65bc8b7.png)


のようなダイアログを表示します。＜CSV＞ボタンと＜EXCEL＞ボタンは、選択したセンサーの環境データをCSVまたはEXCELファイルに保存します。＜CSV＞ボタンと＜EXCEL＞ボタンは、v1.5.0以降で対応です。

![](/images/books/twsnmpfc-manual/picture_pc_f76eaa9f28197c2f71935340bca220b72.png)

＜削除＞ボタンをクリックすると、

![](/images/books/twsnmpfc-manual/picture_pc_b97163a97cf49a169f33f86d0e405175.png)


のような確認ダイアログを表示します。＜削除＞ボタンをクリックするとレポートから削除します。

#### ③ディスプレーフィルター
リストの表示をアドレス、名前、受信ホストに入力した文字列を含むものにフィルター表示できます。

#### ④＜グラフと集計＞ボタン
クリックするとグラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_c4575944cb8e9106c31c77e654d0865f.png)

#### ⑤＜CSV＞ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL>ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
リストを最新の情報に更新します。

# 時系列３Dグラフ

![](/images/books/twsnmpfc-manual/picture_pc_dd59c27c4823f1de502112a1a82c023f.png)

X軸にセンサー、Y軸に時刻、Z軸の項目は右上で選択した３Dのグラフです。選択項目は、気温、湿度、気圧など環境センサーが対応しているものです。

# 時系列２Dグラフ

![](/images/books/twsnmpfc-manual/picture_pc_71fae8470744a458bbd22cee1e0ebfea.png)

３Dのグラフを２Dにしたものです。細かな部分を拡大して確認できます。

# 環境センサーレポートを表示するためには

オムロンまたはSwitchBotの環境センサーとtwBlueScanが必要です。

