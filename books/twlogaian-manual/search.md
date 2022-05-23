---
title: "ログを検索する"
---



ログを読み込んで全文検索エンジンのインデックスを作成できたらログを検索することができます。

![](/images/books/twlogaian-manual/2022-05-24_05-19-03.png)

の赤枠の部分です。


# ログ検索の基本

インデックスの作成が終わった直後は、

![](/images/books/twlogaian-manual/2022-05-24_05-21-01.png)

のような画面になります。

インデックスに読み込んだログの件数や処理時間が右上に表示されます。
ログ検索の基本は上のほうにある検索文の欄に

https://blevesearch.com/docs/Query-String-Query/

の構文で検索文を入力して＜検索＞ボタンをクリックします。
空欄で検索すると全件検索する*を入力したのと同じ動作にしています。
なんとなく、その方が自然だと思ったからです。


# 検索条件を指定する

Bleveの検索構文は初心者にはちょっと難しいかもしれません。
そこで検索文を作るためのGUIを付けてあります。検索文の横にある下矢印ボタン

![](/images/books/twlogaian-manual/2022-05-24_05-23-42.png)

をクリックすれば検索条件を指定する画面が表示されます。


![](/images/books/twlogaian-manual/2022-05-24_05-25-20.png)

同じ場所にある上矢印ボタンで閉じることができます。
検索条件を設定する操作の基本は条件を入力して右側にある＜＋＞ボタンをクリックすることです。
ボタンをクリックした時に検索文に変換して検索文欄に入力されます。

## 検索期間

ログを検索する時間範囲を指定します。

## キーワード

ログ全体や特定の項目（フィールド）に含まれるキーワードを指定します。
判定の条件に、

![](/images/books/twlogaian-manual/2022-05-24_05-26-59.png)

の３種類あります。
含まれるは、キーワードがあれば検索のスコアが高くなりますが、必ずしもキーワードがなくてもよいですが、
必須は、キーワードが含まれていないログは除外されます。

## 数値判定

ログから抽出した数値データの判定条件を指定します。サイズが１００より大きいとかです。

## IP位置情報

実際に使えるかどうかわかりませんが、機能としては面白いので付けたものです。
IPアドレスから位置情報を取得している場合に、位置が指定した緯度経度からの距離の範囲で検索できます。
東京から１００Km圏内とかです。

## 最大件数

検索する時の最大件数を指定します。この項目は、検索文に入力しません。

## 異常ログ検知方法

AI（機械学習）で検索したログの中から異常ログを検知します。検知するためのアルゴリズムは、

![](/images/books/twlogaian-manual/2022-05-24_05-32-26.png)

があります。

検知しない以外を選択した場合に、

![](/images/books/twlogaian-manual/2022-05-24_05-34-06.png)

のように特徴量の計算方法を選択できます。

ログから抽出した数値データや文字列、SQLインジェクションに使わるキーワードの数などが指定できます。
曜日と時間帯は、ログのタイムスタンプから曜日と24時間制の時間帯を計算して特徴量に加えるというものです。
例えば、サーバーの負荷の数値は日曜の夜中は低いけど月曜の朝は高いというような特徴があると思って付けたものです。


# 検索結果の表示

検索文を入力して検索を実行すると結果が

![](/images/books/twlogaian-manual/2022-05-24_05-35-41.png)

のように表示されます。

## グラフの時間範囲と連動

グラフの時間範囲を変更するとログのリストも連動して表示するログを変えます。

![](/images/books/twlogaian-manual/2022-05-24_05-37-40.png)

グラフの右上のズームボタンを押せばグラフをドラックして範囲を指定できます。

## キーワードでフィルター

キーワードに文字列を入力すれば、ログの中に含まれる文字列でフィルター表示できます。

![](/images/books/twlogaian-manual/2022-05-24_05-38-53.png)

## ログの表示形式

検索結果の下にログの表示形式を選択する項目があります。これを切り替えるとリストの表示形式を変えることができます。

![](/images/books/twlogaian-manual/2022-05-24_05-40-29.png)

### タイムオンリー

時刻、検索スコア、ログの行だけの表示です。


![](/images/books/twlogaian-manual/2022-05-24_05-41-35.png)

左側のチェックボックスにチェックしてログを選択すると、クリップボードにコピーやメモに保存できます。

### syslog

syslogに特化した表示です。syslog形式で情報を抽出していないログでは表示できません。

### アクセスログ

アクセスログに特化した表示形式です。アクセス形式で情報を抽出していないログでは表示できません。

![](/images/books/twlogaian-manual/2022-05-24_05-43-07.png)

### 抽出データ

ログから抽出したデータをテーブル形式で表示します。

![](/images/books/twlogaian-manual/2022-05-24_05-44-19.png)

項目が多い時には横スクロールできます。

### 異常ログスコア

タイムオンリーと似ていますが、スコアの部分が異常スコアになります。
選択してコピーメモもできます。
異常ログの検知をONにした場合だけ表示されます。

![](/images/books/twlogaian-manual/2022-05-24_05-45-45.png)

## エクスポート

検索結果の下のほうにエクスポートの選択項目があります。

![](/images/books/twlogaian-manual/2022-05-24_05-47-27.png)

### CSV

CSVファイルに表示しているリストを保存します。

### Excel

Excelファイルに表示しているリストとグラフの画像を保存します。

### ログ種別定義

ログから情報を抽出するために使ったGrokの設定などを定義ファイルに保存するためのものです。
編集して他の分析でも使えるようにするための機能です。

## 処理結果

インデックスの作成やAIの学習状況を後から確認するための画面を表示します。


![](/images/books/twlogaian-manual/2022-05-24_05-48-53.png)

![](/images/books/twlogaian-manual/2022-05-24_05-49-51.png)

