---
title: "Influxdb設定"
---

Grafanaと連携してダッシュボードを表示するためにTWSNMP FCのデータをInfluxdbへ送信するための設定です。Grafanaと連携については

https://note.com/twsnmp/n/nf8500c9f4b49

の記事をみてください。


# Influxdb設定画面の表示方法
メニューの「システム設定」ー「Influxdb」をクリックしてください。

![](/images/books/twsnmpfc-manual/picture_pc_c8ebe5b14b42b10a4db6789ce127e706.png)

# Influxdb設定画面

![](/images/books/twsnmpfc-manual/picture_pc_c8f68c5f3f4d649ae8aa5bd83a0ff2bb.png)

のような感じです。

## URL
InfluxdbにアクセスするためのURLを設定します。

## ユーザーID/パスワード
InfluxdbにアクセスするためのユーザーIDとパスワードを設定します。
Influxdb側の設定で認証なしにしている場合は空欄でよいです。

## データベース
Influxdb側のデータベースの名前を指定します。

## 保存期間
Influxdb側のデータの保存期間を指定します。（１週間から無期限）

## ポーリングログ
ポーリングログの送信について設定します。ポーリングの設定でAI分析かログを保存する設定になっているものだけ送信する場合は「ログのみ送信する」、
全てのポーリングの結果を送信する場合は「全て送信する」を選択してください。送信しない時は当然「送信しない」に設定してください。

## AI分析結果
AIの分析結果を送信する場合に「送信する」に設定してください。
異常スコアをダッシュボードに表示できるようになります。

## ＜初期化＞ボタン
Influxdbのデータベースを初期化するためのボタンです。クリックすると

![](/images/books/twsnmpfc-manual/picture_pc_36d49b2719289c565e373811e24838cb.png)

のような確認ダイアログを表示します。＜初期化＞ボタンをクリックすると実行します。

