---
title: "Windowsログオンレポート"
---

twWinlogセンサーで収集したWindowsマシンへのログオン状況のレポートについての説明です。v1.5.0で忘れていた機能を追加しています。

# Windowsログオンレポートの表示方法
メニューの「レポート」ー「Windows分析」ー「ログオン」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_7b47fa4dea9c7393ce0355955c7022bf.png =100x)


# Windowsログオンレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_7f9086b6a467bf7d1282158034a746b3.png)

のような感じです。

#### ①ログイン状況リスト
Windowsマシンへのログオン状況を示すリストです。
信用スコア、ログオン先、コンピュータ、接続元、記録回数、ログオン回数、ログオフ回数、失敗回数、操作ボタンがあります。

#### ②操作ボタン
＜詳細＞ボタンと＜削除＞ボタンがあります。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_bfb5b57086ee35a0ce3ac945880fa2d0.png)

のようなダイアログを表示します。ログイン状況の詳細がわかります。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_7616826ec3c10115171a3a5c4de7da86.png)

のような確認ダイアログを表示します。＜削除＞ボタンをクリックすれば削除できます。

#### ③ディスプレイフィルター
リストの内容をログオン先、コンピュータ、接続元に入力した文字列を含む項目に絞って表示できます。

#### ④＜グラフと集計＞ボタン
クリックするとグラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_fba973c6137eb0443952774a771169a1.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
信用スコアを再計算するためのボタンです、クリックすると確認ダイアログを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_da2c50ba3b639692de62c1d92cadd59f.png)

#### ⑧＜更新＞ボタン
リストの内容を最新の情報に更新します。

# グラフ分析
接続元とログオン先の関係を力学モデルか円形のグラフで表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_a2c8d075b5bfc470490029416cd6156c.png)

# ３D集計
接続元、ログオン先と回数の関係を３Dのグラフで表現したものです。信用スコアは色で表します。

![](/images/books/twsnmpfc-manual/picture_pc_bcb11e882d58335baa25f81d6b21f44a.png)

# Windowsログオンレポートを表示するためには
twWinlogセンサーをWindowsマシンにインストールしてsyslogをTWSNMP FCに送信する必要がありまます。


