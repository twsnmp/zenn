---
title: "AI分析"
---




TWSNMP FCのAI分析結果を表示するための画面についての説明です。この画面で表示するAIは、

https://note.com/twsnmp/n/n70d2f935c1d3

とか

https://note.com/twsnmp/n/n747ffd303b55

で考えたLocal Outlier Factor (LOF)による異常検知です。
言葉の使い方に厳しい人だとAIではなく機械学習だと怒られそうです。

ポーリング詳細で表示できるBrain.jsを使ったものより安定して分析できると思います。

**v1.10.0からIsolation Forestによる異常検知にも対応しました。**

# AI分析アルゴリズムの設定

マップ設定の画面にAIアルゴリズムの設定があります。
![](/images/books/twlogaian-manual/2022-07-13_06-18-08.png)

# AI分析リスト画面を表示する
メニューの「AI分析」をクリックします。

![](/images/books/twlogaian-manual/picture_pc_55d7178686fe6bbb474d920576db963b.png)

# AI分析リスト画面の構成

![](/images/books/twlogaian-manual/picture_pc_aeb367a0ba5b881ce329612340e6d5f3.png)

のような画面です。

#### ①AI分析リスト
AI分析をしているポーリングのリストを表示します。AIが分析した異常スコア、関連するノード、ポーリング名、分析したデータ数、最後に分析した日時が表示されます。項目をクリックすると並べ替えができます。
このリストに表示されるのは、ポーリングの設定でログモードをAI分析に設定した場合です。ただし、分析に必要なデータ量が集まらないと分析を行いません。

#### ②検索フィルター
リストの項目に含まれる文字列でフィルター表示できます。

#### ③操作ボタン

![](/images/books/twlogaian-manual/picture_pc_709649f1b48f355dd719ca69b3f596d6.png)

左から＜詳細＞、＜マップ＞、＜ポーリング＞＜削除＞のボタンです。
＜マップ＞ボタンをクリックすると関連するノードを選択したマップ画面に移動します。＜ポーリング＞ボタンをクリックすると関連するポーリング情報の画面に移動します。

＜削除＞ボタンをクリックすると

![](/images/books/twlogaian-manual/picture_pc_7a04f7628d035ec9e005fd2027b48b7e.png)

の確認ダイアログが表示されます。＜削除＞をクリックするとAI分析結果を削除します。

# AI分析詳細画面

AI分析のリストから＜詳細＞ボタン（目のアイコン）をクリックするか、ポーリングのリスト画面の操作で＜AI分析＞（脳のアイコン）をクリックすることで表示できます。

![](/images/books/twlogaian-manual/picture_pc_007b2ad4042d5c5f10196dc37be1e3ef.png)

のような画面です。時間帯別の異常スコアのリストです。デフォルトでは、異常スコアの高い順に並んでいます。操作の目のアイコンをクリックすると
関連するポーリングのグラフが表示されます。上の例で、一番悪い異常スコアをポーリングを表示すると

![](/images/books/twlogaian-manual/picture_pc_13f160d5e9a518a59babcf8419c4ba09.png)

のようなグラフになります。応答時間が妙にかっかているのがわかります。
右上の検索フィルターで時間帯などの絞ることができます。
＜グラフ表示＞をクリックするとサブメニューが表示されます。

# ヒートマップ
日と時間帯毎の異常スコアを色で表したヒートマップを表示します。

![](/images/books/twlogaian-manual/picture_pc_78b1997a6f6f847d8441921445fd40ef.png)

赤い場所が異常ということです。

# 異常割合
異常スコアを正常、注意、異常の３段階で集計した円グラフです。

![](/images/books/twlogaian-manual/picture_pc_9e3c0ad68aa94f928571eb301b101c6d.png)

# 時系列
異常スコアを時系列で表示したグラフです。

![](/images/books/twlogaian-manual/picture_pc_928f200fbae5030d37e3f917de0dda2d.png)

