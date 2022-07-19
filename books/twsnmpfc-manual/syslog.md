---
title: "syslog"
---

# syslog画面の表示方法
メニューの「ログ」ー「syslog」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_689594784116a6af44401c92f8e7dd04.png)

# syslog画面

![](/images/books/twsnmpfc-manual/picture_pc_521fa4817cf8b9890420a02871ec6d26.png)

のような感じです。syslogから抽出した情報がある場合は、

![](/images/books/twsnmpfc-manual/picture_pc_c682a3732968917dd05cc63be15d3238.png)

のような感じです。

#### ①グラフ
syslogの状態別の件数を時系列で集計したグラフです。下部のバーで表示する時間範囲を変更できます。凡例をクリックすれば、状態別の表示/非表示を切り替えできます。

#### ②syslogリスト
syslogの状態、日時、種別(PRI)、送信元のホスト名、タグ、メッセージのリストです。項目名をクリックすれば並べ替えができます。

#### ③表示フィルター
種別、送信元ホスト名、タグ、メッセージに含まれる文字列でフィルターできます。（データストアから検索する時に条件を指定するだけだと、検索に毎回時間がかかるので表示する時にフィルターできたほうが便利だと思ってこういう機能をつけています。）

#### ④＜検索条件＞ボタン
クリックすると

![](/images/books/twsnmpfc-manual/picture_pc_82ff9740aaa20a01bd9fba733b4a28a4.png)

のようなダイアログが表示されます。状態と期間は選択して指定します。種別、ホスト名、タグは正規表現で指定します。
メッセージは、パイプラインの正規表現で指定します。パイプラインの正規表現は、

- |で区切る
- !で始まるものは条件を反転（一致しないものという意味）
- |を含む正規表現の場合は、`（バッククオート）で括る

というルールです。

```
test|!bad|`(hehe|fufu)`
```

のように書くとtestを含む行でbadを含まない行、heheかfufuを含む行を探してくれます。
抽出パターンを選択するとsyslogから情報を抽出してくれます。

#### ⑤＜CSV＞ボタン
syslogをCSVファイルに保存します。

#### ⑥＜EXCEL>ボタン
syslogをEXCELファイルに保存します。

#### ⑦グラフと集計
syslogの情報からグラフを表示します。マニュアルを書いている時点では

![](/images/books/twsnmpfc-manual/picture_pc_3caa92499bd2e5a9aa18d3a2699dc534.png)

です。

#### ⑧＜AIアシスト＞ボタン
AIがsyslogの分類をAIがアシストする機能の画面を表示します。

![](/images/books/twsnmpfc-manual/picture_pc_beb7848848635f8becd55c21411ba2be.png)

Brain.jsを使ったものです。それほど賢くないので期待しないでください。
使い方は、

![](/images/books/twsnmpfc-manual/picture_pc_051d12ccfabb47aa5464f3d75f05d9d1.png)

AIに何か教えたいログをチェックします。＜教育＞ボタンをクリックして

![](/images/books/twsnmpfc-manual/picture_pc_f4e452bc5ba2446dd034efc22bfc489c.png)

のダイアログで、このログの分類を教えます。＜分析＞ボタンをクリックしてしばらくすると、

![](/images/books/twsnmpfc-manual/picture_pc_20f698bb031ab9ef5d0ee7d88f7552f3.png)

のように類似しらログに同じ分類の名前をつけてくれます。このAIはゆとり教育世代なのであまり大量に学習させると固まってしまうので注意してください。

#### ⑨＜更新＞ボタン
syslogを前回と同じ条件で再検索して表示します。

#### ⑩＜抽出情報＞ボタン
検索条件で抽出パターンを指定して検索した結果にsyslogから抽出した情報がある場合にこのボタンが表示されます。クリックすると抽出した情報を表示することができます。

![](/images/books/twsnmpfc-manual/picture_pc_4f5ad6e02f2ad72ec908a712ed27a8af.png)

抽出した情報を＜CSV＞ボタン、＜EXCEL＞ボタンをクリックしてファイルに保存することができます。＜グラフと集計＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_9a157d542d68a466d5675dda8bba4566.png)

のメニューが表示されます。

# ヒストグラム
優先度、ファシリティなどで集計したヒストグラムです。

![](/images/books/twsnmpfc-manual/picture_pc_346cf1efea50c2dbff06d4df74e584d0.png)

# クラスター分析
優先度とファシリティをクラスター分析し結果です。

![](/images/books/twsnmpfc-manual/picture_pc_07a52f77f1e9b4473566219427ad8a19.png)

# ホスト別
syslogの件数をホスト別に集計したグラフとリストです。CSVやEXCELに保存できます。

![](/images/books/twsnmpfc-manual/picture_pc_eb68af4897e286a46c857b377b2c153f.png)

# ホスト別３D
ホスト別の集計を３Dのグラフで表したものです。

![](/images/books/twsnmpfc-manual/picture_pc_7552c737bb052cf091a9917d1971deed.png)

# FFT分析
syslogが送信される周期をFFTで分析したグラフです。総数とホスト別の切り替えができます。周波数の表示もできます。

![](/images/books/twsnmpfc-manual/picture_pc_c4fed219b91b26574f00677c0719a40e.png)

# FFT分析（３D)
FFTの分析結果を３Dのグラフで表したものです。

![](/images/books/twsnmpfc-manual/picture_pc_613bda0f411a9905511856d5667d6920.png)

# 抽出情報のヒストグラム分析
抽出した情報のうち数値データをヒストグラムで表示します。

![](/images/books/twsnmpfc-manual/picture_pc_9c5c0ce867c27557ff666f00f83e03e6.png)

この例は1分毎の負荷(Load Avg.)をヒストグラムにしたものです。負荷の分布がほとんどが０．１から０．５ぐらいで高い時で２．７があるという様子がわかります。

# 抽出情報のクラスタ分析
抽出した情報のうち数値データをクラスター分析して表示します。

![](/images/books/twsnmpfc-manual/picture_pc_e074cdf9e0a6075818d0329c3a1dedfa.png)

# 抽出情報の項目別集計
抽出した情報を項目別に集計します。

![](/images/books/twsnmpfc-manual/picture_pc_ab3f45ac2044cdbdcc600bfdc5fe5f0b.png)

この例では抽出したログの件数をホスト別に集計しています。＜CSV>＜EXCEL>ボタンでファイルの保存することもできます。

# 抽出情報の項目別集計（３D）
抽出した情報を項目別に集計して３Dのグラフで表示します。

![](/images/books/twsnmpfc-manual/picture_pc_2cfbd61a40c42dcf5306cf71e93b9919.png)

上部にある選択項目でX軸、Z軸、色付けに使う項目を選択できます。
この例ではX軸がホスト、Z軸が１分間負荷、色分けが５分間負荷になっています。miniPCというホストの負荷が高くなっている様子がわかります。

# syslog画面を開発中の記事
syslog分析画面を開発中に書いた苦労話の記事をリストアップしておきます。
どうしてこんな仕様なのか理由がわかるかもしれません。

https://note.com/twsnmp/n/ne53b792c9d7d

https://note.com/twsnmp/n/n829f1a0e111c

https://note.com/twsnmp/n/nd50667de7089

https://note.com/twsnmp/n/n395e9e5e9419

