---
title: "Windowsプロセスレポート"
---
twWinlogセンサーで収集したWindowsマシンで起動したプロセスに関するレポートの説明です。Windowsマシンで誰がどんなプロセスを起動したか調べることができます。セキュリティーの調査に役立つと思います。


# Windowsプロセスレポートの表示方法
メニューの「レポート」ー「Windows分析」ー「プロセス」をクリックすれば表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_bff7aecdd7d5cd0692d63502fb6dcd34.png =100x)

# Windowsプロセスレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_ce78c6634741a2a93172a2d0e48ad1ef.png)

のような感じです。

#### ①プロセスリスト
Windowsマシンで起動・停止したプロセスのリストです。
項目には最後の終了ステータス、コンピュータ、プロセス名、操作アカウント、起動回数、停止回数、操作ボタンがあります。
終了スタータスが０ｘ０は青いアイコン、それ以外は赤いアイコンを表示しています。プロセスが正常終了した場合の終了ステータスが０ｘ０が多いためです。それ以外は異常ということです。

#### ②操作ボタン
＜詳細＞ボタンと＜削除＞ボタンがあります。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_35a6cff148c4d31c9883079658b8d24a.png)

のようなダイアログを表示します。ログイン状況の詳細がわかります。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_f50cbdead09432cd523a5496fee3e499.png)

のような確認ダイアログを表示します。＜削除＞ボタンをクリックすれば削除できます。

#### ③ディスプレイフィルター
リストの内容をコンピュータ名、プロセス名に入力した文字列を含む項目に絞って表示できます。

#### ④＜グラフと集計＞ボタン
クリックするとグラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_0d39631d847fde2ec77150ac32a48b8f.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
リストの内容を最新の情報に更新します。

# グラフ分析
コンピュータとプロセス名、操作アカウントとプロセス名、親プロセスとプロセス名の関係を力学モデルまたは円形のグラフで表現します。

![](/images/books/twsnmpfc-manual/picture_pc_e2efe5b55d1c364aabeeab0cd049abc7.png)

![](/images/books/twsnmpfc-manual/picture_pc_9bc540f553725c0fd941dd63121d97c9.png)

のような感じです。

# ３Dグラフ
コンピュータとプロセス名、操作アカウントとプロセス名、親プロセスとプロセス名の関係を３Dのグラフで表現します。

![](/images/books/twsnmpfc-manual/picture_pc_131cfb8fc2f496562389a0d1622da3cd.png)

右上の項目を変更するとグラフの表示に反映されます。

# Windowsプロセスレポートを表示するためには
twWinlogセンサーをWindowsマシンにインストールしてsyslogをTWSNMP FCに送信する必要がありまます。


