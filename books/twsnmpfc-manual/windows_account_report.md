---
title: "Windowsアカウント操作レポート"
---


twWinlogセンサーで収集したWindowsマシンのアカウント操作に関するレポートの説明です。Windowsマシン上でアカウントの作成、変更やパスワードの変更の操作を行ったことを集計できます。


# Windowsアカウント操作レポートの表示方法
メニューの「レポート」ー「Windows分析」ー「アカウント」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_9b0f485b1580f13cbb20332f600deedd.png =100x)

# Windowsアカウント操作レポート画面

![](/images/books/twsnmpfc-manual/picture_pc_d2cc0b5bb5f8023ac9c638f5c71665c5.png)

のような感じです。

#### ①アカウント操作リスト
Windowsマシン上でアカウントの操作を集計したリストです。
操作アカウント、対象アカウント、コンピュータ、回数、編集の回数、パスワード変更の回数、その他の操作の回数、最後に操作した日時、操作ボタンがあります。

#### ②操作ボタン
＜詳細＞ボタンと＜削除＞ボタンがあります。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_d713a224081def5670d1acce6b19ccf8.png)

のようなダイアログを表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_59d30ac1135c8a85d0ebd8bbbc83dc05.png)

の確認ダイアログを表示します。＜削除＞ボタンをクリックすれば削除できます。

#### ③ディスプレーフィルター
リストの内容を操作アカウント、対象アカウント、コンピュータに入力した文字列を含むものに絞って表示できます。

#### ④＜グラフと集計＞ボタン
グラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_fa193ae964cfc8992a17b4c83c629637.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
リストの内容を最新の情報に更新します。

# グラフ分析
操作アカウントと対象アカウントの関係を力学モデルか円形のグラフで表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_395d21a17fb6a35ad2c0a4deb41612f9.png)

回数の多さはラインの色と太さで表現しています。

# ３D集計
操作アカウント、対象アカウントと回数の関係を３Dのグラフで表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_f556a2a83debd24521f1c009c7a6508a.png)

