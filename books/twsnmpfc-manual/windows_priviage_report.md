---
title: "Windows特権アクセスレポート"
---

twWinlogセンサーで収集したWindowsの特権アクセスレポートの説明です。
管理対象のWindowsマシン上で管理者権限の操作が行われた回数を調べることができます。セキュリティーのための機能です。

# Windows特権アクセスレポートの表示方法
メニューの「レポート」ー「Windows分析」ー「特権アクセス」をクリックすれば表示できます。

# Windows特権アクセスレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_0cf3c9353f10ed901fefc10f959ae6d4.png)

のような感じです。

#### ①特権アクセス状況リスト
Windowsマシンへの特権アクセス状況を示すリストです。
項目として操作アカウント、コンピュータ、回数、最後に検知した日時、操作ボタンがあります。

#### ②操作ボタン
＜詳細＞ボタンと＜削除＞ボタンがあります。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_a9766f9b5d2f254bc80dacd97c8a3f0d.png)

のようなダイアログを表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_1546845cff81dd42bd24a2c3bfb68764.png)

のような確認ダイアログを表示します。＜削除＞ボタンをクリックすれば削除できます。

#### ③ディスプレイフィルター
リストの内容を対象アカウント、コンピュータに入力した文字列を含む項目に絞って表示できます。

#### ④＜グラフと集計＞ボタン
クリックするとグラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_f04afcfc81635ca3c6f1883c616f358f.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
リストの内容を最新の情報に更新します。

# ３Dグラフ
対象アカウント、コンピュータと回数の関係を３Dのグラフで表現します。

![](/images/books/twsnmpfc-manual/picture_pc_adf0124f8ade3c6e6f16a56fbcf7aae1.png)

# Windows特権アクセスレポートを表示するためには
twWinlogセンサーをWindowsマシンにインストールしてsyslogをTWSNMP FCに送信する必要がありまます。

