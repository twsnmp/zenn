---
title: "サーバーレポート"
---

NetFlowなどからTWSNMP FCが見つけたサーバーの情報を表示するサーバーレポート画面の説明です。


# サーバーレポート画面の表示方法
メニューの「レポート」ー「NetFlow分析」ー「サーバー」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_0d2aaebb7ca4cdff73c82cd147e38f1a.png)

# サーバーレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_da7df5a73d6d1299f47dda4cb57df3f5.png)

のような感じです。

#### ①リスト

TWSNMP FCが見つけたサーバーのリストです。信用スコア、サーバー名、国、サービス概要、検知した回数、通信量、最後に検知した日時、操作ボタンがあります。サービス概要は一般的なサービス名（WEBやMAIL）をカンマ区切りで表現して最後のカッコ内の数値で詳しいサービスの数を示しています。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_d255dcfe09ed1f46b50777437a2f77c4.png)

左から＜マップ＞ボタン、＜アドレス分析＞ボタン、＜詳細＞ボタンです。マップに管理対象ノードとして登録されていないサーバーには＜マップ＞ボタンは表示されません。＜マップ＞ボタンをクリックするとマップ画面を表示した選択したサーバーに対応するノードを表示します。
＜アドレス分析＞ボタンはサーバーのIPアドレスについて調査するためのアドレス分析画面を表示します。
＜詳細＞ボタンをクリックするとノードの詳細情報のダイアログを表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_320f070f1817930f08e99b2fa0f08274.png)

のような確認のダイアログを表示します。＜削除＞ボタンをクリックすると削除できます。

#### ③ディスプレーフィルター
サーバー名、国名、サービス概要に入力した文字列を含むものでフィルター表示できます。

#### ④＜グラフ表示＞ボタン
サーバーに関するグラフのメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_1f3fa2af439fe51aca8b245bada1a7d7.png)

#### ⑤＜CSV>ボタン
サーバーリストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
サーバーリストの内容をEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
クリックすると

![](/images/books/twsnmpfc-manual/picture_pc_24bc0fbe78f2ba198dbd67991453fbe9.png)

のような確認のダイアログを表示します。＜実行＞ボタンをクリックすると信用スコアを再計算します。

#### ⑧＜更新＞ボタン
サーバーリストの内容を最新の情報に更新します。

# サーバー詳細画面

![](/images/books/twsnmpfc-manual/picture_pc_668de83260695a096167344fac06a322.png)

のような感じです。サーバーに関する詳しい情報を表示します。IPアドレスから位置情報がわかっている場合はGoogle Mapで地図を表示するボタンが表示されます。twpcapセンサーでTLS通信、NTPサーバーなどを取得した場合は、この画面に表示されます。
＜サービス割合＞ボタンをクリックすると対象のサーバーが提供するサービスの通信量の割合を表示します。

![](/images/books/twsnmpfc-manual/picture_pc_20cedae4ec4554fdf3fcc8e53028023f.png)

このグラフの元情報は、

![](/images/books/twsnmpfc-manual/picture_pc_2f650e738d8a241e06b705f184dbc3c6.png)

のサービス詳細の部分です。
＜マップに追加＞ボタンをクリックすると対象のサーバーを管理マップに追加するためノード編集のダイアログを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_19de8aac91ecfb51040a4c76b4dc577a.png)

ノードの情報を入力して＜保存＞ボタンをクリックすればマップに追加できます。

# サーバー位置グラフ
サーバーの位置を世界地図に表示します。

![](/images/books/twsnmpfc-manual/picture_pc_41a4affdcdda3a8f25af0133129c078e.png)

IPアドレスから位置情報を取得するためのGeoIPのデータベースを登録する必要があります。

# 国別グラフ
サーバーを国別に集計したグラフを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_4d418e9b6c851053ec0434744f283d5d.png)

サーバーレポートを表示するためには？
サーバーレポートの情報はNetFlowまたはIPFIXのデータが必要です。NetFlowに対応したネットワーク機器（Firewall/SW-HUBなど）かLinuxにsoftflowdをインストールしてNetFlowのデータを送信する方法もあります。

https://hub.docker.com/r/twsnmp/softflowd

が便利です。

