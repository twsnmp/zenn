---
title: "RADIUS通信レポート"
---

twpcapセンサーで収集したRADIUS通信の状況を示すレポートについての説明です。RADIUS通信は無線LANのアクセスポイントやVPNルーターと認証サーバーの間で認証のために行われるものです。無線LANやVPNルーターに不正なアクセスが増えたことを調べることができます。


# RADIUS通信レポートの表示方法
メニューの「レポート」ー「パケット分析」ー「RADIUS通信」をクリックすれば表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_309a3f1d09d247e06c25640c86aa6f74.png)

# RADIUS通信レポート画面

![](/images/books/twsnmpfc-manual/picture_pc_0041fe51ab54afa3ef7e1c31d73fadf1.png)

のような感じです。私の家のネットワークではRADIUSで認証を行っていないので画面の例がしょぼいです。

#### ①RADIUS通信リスト
RADIUSクライアント（無線LANのアクセスポイントやVPNルータ）とサーバー（認証サーバー）間のRADIUS通信のリストです。
信用スコア、クライアント、サーバー、レポート回数、認証の成功率、リクスエストの回数、チャレンジの回数、アクセプトの回数、リジェクトの回数、最後の検知した日時、操作ボタンがあります。
信用スコアは、この組み合わせの通信が他の通信と比較してどうかを示す偏差値になっています。５０が平均という意味です。
リストの項目をクリックすれば、並べ替えできます。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_f3e73f2c35246a359d0affe0d5465588.png)

左から＜アドレス分析＞ボタン、＜詳細＞ボタン、＜削除＞ボタンです。
＜アドレス分析＞ボタンをサーバーのIPアドレスについてアドレス分析で調べます。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_0e319ea3d7a5c2189fb5df752afded8a.png)

のような詳細情報のダイアログを表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_a31c5a2d1744a8ea64d6cb6c1cb449c5.png)

の確認ダイアログを表示します。＜削除＞ボタンをクリックすれば削除できます。

#### ③ディスプレーフィルター
リストの内容をサーバー、クライアントに入力した文字列を含むものにフィルター表示できます。

#### ④＜グラフと集計＞ボタン
グラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_1c325306b598bee492b69227eebb4e8c.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
信用スコアを再計算するためのボタンです、クリックすると確認ダイアログを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_f4421972cd55d67071772c92a583f558.png)

#### ⑧＜更新＞ボタン
リストの内容を最新の情報に更新します。

# グラフ分析
クライアントとサーバーの関係を力学モデルか円形のグラフで表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_f9fbf87381b4517a0b7e4f94fd89bb2e.png)

# クライアント別
クライアント別にアクセプトとリジェクトの割合を表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_b0b96e7dd82853a3c4a1a191d5385984.png)

# サーバー別
サーバー別にアクセプトとリジェクトの割合を表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_872d45ff57a83e05e625327559a67259.png)

# クライアント/サーバー間
クライアントとサーバー間のアクセプトとリジェクトの割合を表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_151aa0eed00fd4453aeebc95ab601d22.png)

# 改善したい項目
今後、グラフを集計に３Dのグラフをつけるなど改善したいと思っています。

