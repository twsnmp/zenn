---
title: "フローレポート"
---

NetFlow/IPFIXのデータをTWSNNP　FCで集計したフローレポートについての説明です。フローレポートはクライアントとサーバーが何の目的でどのくらい通信しているかを調べるためのものです。


# フローレポート画面の表示方法
メニューの「レポート」ー「NetFlow分析」ー「フロー」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_6b171c00957649480449626442b0add3.png)

# フローレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_ea4f0d504a1ef49b24b758c7e01a6b0b-1.png)

のような感じです。

#### ①リスト
通信フローのリストです。信用スコア、クライアント、サーバー、サーバーの国、サービス概要、検知回数、通信量、最終検知日時と操作ボタンがあります。信用スコアはフローレポートの中で相対的に信用できる通知であることを偏差値で表しています。偏差値が低いものに注意すればよいということです。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_32d88d98ab07b3db32ba6ef55d3f808b.png)

左から、＜マップ＞ボタン、＜アドレス分析＞ボタン、＜詳細＞ボタン、＜削除＞ボタンです。
＜マップ＞ボタンは、クライアントかサーバーがTWSNMP　FCに登録されたノードの場合に表示されます。クリックするとマップ画面を表示して対応するノードを選択状態にします。＜アドレス分析＞ボタンはサーバーのIPアドレスをアドレス分析で調査します。
＜詳細＞ボタンをクリックすると通信フローの詳細画面を表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_f445f0ede0e4b93bf8339ca1d66db036.png)

のような確認のダイアログを表示します。＜削除＞ボタンをクリックすれば、フローを削除できます。

#### ③ディスプレーフィルター
クライアント名、サーバー名、国名、サービス概要に入力した文字列を含むものでフィルター表示できます。

#### ④＜グラフと集計＞ボタン
サーバーに関するグラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_d8324982e5416e2e515c11b670102b6f.png)

#### ⑤＜CSV>ボタン
フローリストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
フローリストの内容をEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
クリックすると

![](/images/books/twsnmpfc-manual/picture_pc_277392859f47664f296a62cff78e53f3.png)

のような確認のダイアログを表示します。＜実行＞ボタンをクリックすると信用スコアを再計算します。信用スコアは数分毎に計算していますが、計算を早めるためのボタンです。

##### ⑧＜更新＞ボタン
フローリストの内容を最新の情報に更新します。

# フロー詳細画面

![](/images/books/twsnmpfc-manual/picture_pc_c427545fa796b308f2ccde337638c067.png)

のような感じです。。位置情報がわかる場合にはGoogle Mapを表示するボタンが表示されます。＜削除＞ボタンをクリックすれば確認ダイアログを表示して、この情報を削除できます。
＜サービス割合＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_ae6a0ac2a6a77840a1e3a8229a8b10ec.png)

のように、サーバーとクライアント間の通信内容がわかります。

# グラフ分析
クライアントとサーバーの関係を力学モデルや円形のグラフで表示します。

![](/images/books/twsnmpfc-manual/picture_pc_a51837cc83b988d425705dde99ae2541.png)

![](/images/books/twsnmpfc-manual/picture_pc_4257a011455f592df57f9cb35479fcad.png)

この例は、サービスをDHCPでフィルター表示した状態で表示したグラフです。DHCPサーバーがローカルに１台しかないことがわかります。

# 地球儀
クライアントとサーバーの通信を地球儀に表示します。

![](/images/books/twsnmpfc-manual/picture_pc_73acae18197b1976a57f8899b1ec727a.png)

IPアドレスから位置情報を取得できるような設定が必要です。

# 国別
フローリストのサーバー位置を国別に集計したグラフです。

![](/images/books/twsnmpfc-manual/picture_pc_c6547bd0c13b13a8375da637513b7e7a.png)

# 不明ポート
ポート番号からサービスの名前がわからないポート番号一覧です。
（どちらかというと私が不明なポートを自分で調べてTWSNMP　FCに登録するための調査用のリストです。）

![](/images/books/twsnmpfc-manual/picture_pc_c0459ce8a6d1b4b4324e86b7595b7492.png)

# フローレポートを表示するためには？
サーバーレポートの情報はNetFlowまたはIPFIXのデータが必要です。NetFlowに対応したネットワーク機器（Firewall/SW-HUBなど）かLinuxにsoftflowdをインストールしてNetFlowのデータを送信する方法もあります。

https://hub.docker.com/r/twsnmp/softflowd

が便利です。

