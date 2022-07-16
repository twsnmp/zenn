---
title: "TLS通信レポート"
---

twpcapにより取得したTLS通信の情報をTWSNMP FCで表示する画面の説明です。管理しているネットワークのパソコンや端末の暗号通信の様子を調べることができます。最近はネットワーク通信のほとんどが暗号（TLS)になっています。TLS通信のバージョンや暗号方式には安全ではないものがあります。それを見つけるのがこのレポートの目的です。


# TLS通信レポート画面の表示方法
メニューの「レポート」ー「TLS通信分析」ー「TLS通信」か「レポート」ー「パケット分析」ー「TLS通信通信」をクリックすれば表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_62c1011c3d5b561142baee3da2ce3a88.png)

2つあるのはサーバー証明書のレポートのメニューが１つだけになるのが寂しいので関連するものをまとめた時に悩んだためです。
もっと良い分類を思いついたら変更するかもしれません。

# TLS通信レポート画面

![](/images/books/twsnmpfc-manual/picture_pc_1702371a2a7662ba3c6358ab74baafdf.png)

のような感じです。

#### ①リスト
twpcapで見つけたTLS通信のリストです。信用スコア、クライアント、サーバー、国、サービス、TLSのバージョン、暗号強度、回数、最初に発見した日時、最後に検知した日時、操作ボタンがあります。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_77ae13053598dbc2c6b3cd58fd8ffcda.png)

左から＜マップ＞ボタン、＜アドレス分析＞ボタン、＜詳細＞ボタン、＜削除＞ボタンです。
＜マップ＞ボタンはクライアントが管理対象のノードに登録されている場合に表示されます。クリックするとマップ画面に移動します。
＜アドレス分析＞ボタンは、サーバーのIPアドレスをアドレス分析で調査するためのボタンです。
＜詳細＞ボタンをクリックすると、

![](/images/books/twsnmpfc-manual/picture_pc_6161a9098dbba3442adcb92b3ea0828f.png)

のような詳細情報のダイアログを表示します。
＜削除＞ボタンをクリックすると、

![](/images/books/twsnmpfc-manual/picture_pc_d5d8dfe68adcfc7c5c9dd4270f4d5d0d.png)

のような確認ダイアログを表示します。＜削除＞をクリックすれば削除できます。

#### ③ディスプレーフィルター
リストの内容を入力した文字列を含むものにフィルター表示します。

#### ④＜グラフと集計＞ボタン
グラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_8e4c6513491b5b484b3edfd52b6f2d94.png)

#### ⑤＜CSV>ボタン
TLS通信リストをCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
TLS通信リストをEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
信用スコアを再計算するためのボタンです。

#### ⑧＜更新＞ボタン
TLS通信リストを最新の情報に更新します。

# グラフ分析
TLS通信のクライアントとサーバー組み合わせを力学モデルか円形のグラフで表示します。

![](/images/books/twsnmpfc-manual/picture_pc_e7fddc63d2bd45215dd881132a75fa0f.png)

表示するリストが多すぎる時は、エラーが表示されます。ディスプレーフィルターで絞ってから表示してください。例えば、メールの通信だけにすると

![](/images/books/twsnmpfc-manual/picture_pc_a4fb509cdd6333efc2e3b95976ca8d75.png)

のような感じで分析できます。

# TLS通信フロー（位置情報）
TLS通信フローを地球儀に表示します。さっきのメールの通信は

![](/images/books/twsnmpfc-manual/picture_pc_4f9de6267cf2f41418910c64ac917eac.png)

のような感じです。

# 国別
サーバーやクライアントの国別の集計です。

![](/images/books/twsnmpfc-manual/picture_pc_eb5a065a72ea9c2cafd09c12e26ad97f.png)

のような感じです。

# TLSバージョン別
TLSのバージョン別の集計です。

![](/images/books/twsnmpfc-manual/picture_pc_f32edaeee07cae813746773ed045c56c.png)

のような感じです。ほとんどTLS１．２か１．３です。

# 暗号スイート別
TLS通信の暗号方式別の集計です。

![](/images/books/twsnmpfc-manual/picture_pc_dfb9b0dd6438adf536185286555834cf.png)

のような感じです。

# 信用スコアの計算方法
v1.5.0から以下の計算にしました。

- サーバーまたはクライアントが禁止国から
- TLSのバージョンが低い（SSL < 1.0 < 1.1 < 1.2 < 1.3）
- 名前解決できないサーバー

の時にペナルティーを増やします。

# TLS通信レポートを表示するためには
twpcapというセンサーからsyslogで情報を送信する必要があります。
