---
title: "Windows Kerberosチケット発行状況レポート"
---

twWinlogセンサーで集めたWindowsサーバーのKerberosチケットの発行に関するレポートの説明です。Windowsサーバーが発行したKerberosのチケットの種類、要求元、成功と失敗の回数をカウントしています。Windowsサーバーに関するセキュリティーの問題を調査するのに役立つと思って作った機能です。

# Windows Kerberosレポートの表示方法
メニューの「レポート」ー「Windows分析」ー「 Kerberos」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_523b48d09153666a7e3df6ca76cbc8d4.png =100x)

# Windows Kerberosレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_1fb3df13dc45fe3b498c6ca9ecee0b8a.png)

のような感じです。

#### ①Kerberosチケット発行状況リスト
WindowsサーバーのKerberosチケットの発行状況に関するリストです。
信用スコア、チケットの対象、コンピュータ、要求元のIPアドレス、サービス、チケットの種類、要求の回数、失敗の回数、最後に検知した日時、操作ボタンがあります。項目をクリックすれば並べ替えできます。

#### ②操作ボタン
＜詳細＞ボタンと＜削除＞ボタンがあります。
＜詳細＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_0773695a2d54dc1cadd0f9064d389fa2.png)

のようなダイアログで詳細な情報を表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_bd4b7d7798f5939b986b0fc66eaa9d27.png)

の確認ダイアログを表示して選択した項目を削除できます。

#### ③ディスプレイフィルター
リストの内容をログオン先、コンピュータ、接続元に入力した文字列を含む項目に絞って表示できます。

#### ④＜グラフと集計＞ボタン
クリックするとグラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_0f042191baee9b5ed61e4495215c0069.png)

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
信用スコアを再計算するためのボタンです、クリックすると確認ダイアログを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_fdf2dc3e6f25b17e0544f6cb1239b33d.png)

#### ⑧＜更新＞ボタン
リストの内容を最新の情報に更新します。

# グラフ分析
チケットの要求元と対象の関係を力学モデルか円形のグラフで表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_34dcaf028264a6deace2259531dda9b0.png)

# ３D集計
チケットの要求元、対象と回数を３Dのグラフで表現したものです。

![](/images/books/twsnmpfc-manual/picture_pc_cbd8bf16fd557e40593d8f71341d328d.png)

# Kerberosレポートについて
このレポート機能は、IPAがサイバー攻撃対策として紹介しているActive Directoryのログ調査に役立つかと思って作ったものです。
https://www.jpcert.or.jp/research/AD.html

私はWindowsのサーバー管理を実際にしていないので、どの程度有効かはわかりません。もし、改善点があれば、教えてください。

