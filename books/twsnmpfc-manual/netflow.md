---
title: "NetFlow/IPFIX"
---

TWSNMP FCで受信したNetFlow/IPFIXの情報を表示する画面の説明です。

# NetFlow／IPFIX画面の表示方法
メニューの「ログ」ー「NetFlow」または「ログ」ー「IPFIX」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_7ae0f97e4cef0e9d09f5798371f7f71c.png)

# NetFlow/IPFIX画面

![](/images/books/twsnmpfc-manual/picture_pc_4985b60f519cf68689bdb86f5c2a0a5e.png)

のような感じです。

#### ①グラフ
NetFlow/IPFIXパケットの受信数をグラフで表示します。

#### ②リスト
受信したフロー情報のリストです。発生日時、送信元、宛先、プロトコル、TCPヘッダのフラグ、パケット数、バイト数、期間の項目があります。項目をクリックすれば並べ替えができます。

#### ③ディスプレーフィルター
送信元、宛先、プロトコル、TCPフラグについて入力した文字列を含むものだけ表示するようにフィルターできます。

#### ④＜検索条件＞ボタン
クリックすると検索条件を指定するダイアログを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_854a73d946bfbef797be4662803e9b36.png)

期間、送信元、宛先のIPアドレスを正規表現で指定します。ポート番号は数値で指定します。これらは送信元、宛先のどちらかが一致すればよいです。
プロトコルとTCPフラグは選択して指定します。一般的だと私が思っている選択肢をいれてあります。不足しているようならばお知らせください。
双方向の指定をオンにすると

![](/images/books/twsnmpfc-manual/picture_pc_5429c56db7f1611504c296dbf8d88ef5.png)

のような画面になります。送信元と宛先のIPアドレスとポート番号を別々に指定できるようになります。

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦グラフと集計
NetFlow/IPFIXの情報をグラフ表示するメニューです。以下のメニューがあります。

![](/images/books/twsnmpfc-manual/picture_pc_f1a8a2d83c6c33741cf0e73bc09a59a8.png)

#### ⑧＜更新＞ボタン
同じ条件でデータストアから再検索してリストを更新します。

# 通信量グラフ
NetFlow/IPFIXのフロー情報を集計して通信量のグラフを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_f45d72d328c24d83db15ef72b0f59656.png)

集計には、バイト数、パケット数とそれぞれの単位時間あたりの値があります。

# ヒストグラム
NetFlow/IPFIXのフロー情報を集計して、平均パケットサイズ、期間、速度に関するヒストグラムを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_8ea9852660a4451ba1b5d5df7fa517a4.png)

# クラスター分析
NetFlow/IPFIXのフロー情報から平均パケットサイズ、速度などの関係をクラスター分析します。

![](/images/books/twsnmpfc-manual/picture_pc_0bc15753a622c34c760f832b7cfe0941.png)

# 送信元別通信量
NetFlow/IPFIXのフロー情報から通信量を送信元別に集計します。

![](/images/books/twsnmpfc-manual/picture_pc_6333567a3632be14484840280f591fef.png)

# IPペアー別通信量
NetFlow/IPFIXのフロー情報から通信量をIPアドレスのペアー別に集計します。

![](/images/books/twsnmpfc-manual/picture_pc_aab7612c7352e7a29e8002605cafc877.png)

# IPペアー別グラフ分析
NetFlow/IPFIXのフロー情報をIPアドレスのペアー別に集計して力学モデルのグラフや円形のグラフで表示します。

![](/images/books/twsnmpfc-manual/picture_pc_6e2a6dbc61be5901e6ac83a59225dd10.png)

# サービス別通信量
NetFlow/IPFIXのフロー情報をサービス別に集計したグラフです。

![](/images/books/twsnmpfc-manual/picture_pc_5c4f20580e90b42a92f7557e24462cbd.png)

# サービス別通信量（３D）
NetFlow/IPFIXのフロー情報をサービス別に集計した３Dのグラフです。

![](/images/books/twsnmpfc-manual/picture_pc_9f69ea17f48127969d76912902cc4f85.png)

# 送信元別通信量（３D)
NetFlow/IPFIXのフロー情報から通信量を送信元別に集計して３Dのグラフにしたものです。

![](/images/books/twsnmpfc-manual/picture_pc_68bea4416f2d1ca4c638dffbf2f1caba.png)

# IPペアー別通信量（３D）
NetFlow/IPFIXのフロー情報から通信量をIPアドレスのペアー別にで集計して３Dのグラフにしたものです。

![](/images/books/twsnmpfc-manual/picture_pc_bbb03362fc03de3b093b63c434b55eb9.png)

# FFT分析
NetFlow/IPFIXのフロー情報からトータルおよび送信元別の回数をFFTで分析したグラフです。周期的な通信を見つけるのに役立つと思って付けた機能です。

![](/images/books/twsnmpfc-manual/picture_pc_d42080a944af288484f5ac2891c9015b.png)

# FFT分析（３D)
NetFlow/IPFIXのフロー情報からトータルおよび送信元別の回数をFFTで分析した３Dグラフです。

![](/images/books/twsnmpfc-manual/picture_pc_41464e630b5b26796b45c9fca6406933.png)

NetFlow/IPFIXを受信するためには
マップ設定でNetFlowの受信設定をオンにします。

画像2

NetFlowとIPFIXは同じポートで受信します。受信したパケットのバージョンによって振り分けます。
TWSNMP FCは **NetFlow v5とIPFIX( NetFlow v10)** にしか対応していません。
NetFlow v9とかは受信しても破棄します。

