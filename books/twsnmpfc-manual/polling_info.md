---
title: "ポーリング情報"
---



TWSNMP FCで実施してるポーリングの結果を確認するポーリング情報画面についての説明です。


# ポーリング情報画面の表示方法

すべてのポーリングリスト画面

![](/images/books/twlogaian-manual/picture_pc_436b81876c0302bfd8c7d3972a0555d3.png)

か、ノード単位のポーリングリスト画面

![](/images/books/twlogaian-manual/picture_pc_1343792ea7f2e115c84beecd426d4f0a.png)

の操作にある目のマークのアイコンをクリックすると表示できます。

# ポーリング情報画面

![](/images/books/twlogaian-manual/picture_pc_09e5c4545f7c10a7d50b29d5e3a9bd85.png)

のような画面です。ノード名、ポーリング名、状態などのポーリングに関する情報が表示されます。
結果欄には、最後に実施したポーリングの結果取得した情報が表示されます。判定スクリプトで使える変数名と値になっています。
ポーリングの結果をログに保存する設定になっている場合には、＜グラフと集計＞と＜ログクリア＞のボタンが表示されます。＜グラフと集計＞をクリックするとサブメニューが表示されます。
＜ログクリア＞ボタンをクリックすると

![](/images/books/twlogaian-manual/picture_pc_806130ec6f8f65b46d0f53e4694155b6.png)

の確認ダイアログが表示されます。＜クリア＞のクリックすれば、ポーリング結果のログをクリアします。

# ポーリングログ

＜グラフと集計＞のサブメニュー「ポーリングログ」を選択した場合に

![](/images/books/twlogaian-manual/picture_pc_5cc28e45a870fa5493c176a515667612.png)

のような画面が表示されます。ポーリングの実行結果の記録です。＜時間範囲＞のボタンをクリックすると

![](/images/books/twlogaian-manual/picture_pc_c29fb17f402f5613483704d088b7eda2.png)

のようなダイアログが表示されて表示するポーリングログの時間範囲を変更できます。範囲を指定しないデフォルトの状態では１週間分表示します。

# 時系列グラフ
ポーリング結果の数値データを時系列グラフで表示します。

![](/images/books/twlogaian-manual/picture_pc_4709a1c2318577bd141a656f9ac05a73.png)

右上のリスト（赤い矢印）で表示する数値データを選択できます。＜時間範囲＞ボタンでポーリングログの表示範囲を変更できます。＜予測＞ボタンは、

![](/images/books/twlogaian-manual/picture_pc_47ab696689ec81b534cd2fd01dfb47ce.png)

表示している数値データの今後の値をを予測するものです。一次関数による近似なので単純に増加か減少傾向にある場合しか、それりの結果を表示しません。ディスクの使用量の増加とかメモリーの空き容量の減少とかには使えると思います。

# ヒストグラム
ポーリング結果の数値データをヒストグラムで表示したグラフです。

![](/images/books/twlogaian-manual/picture_pc_0d9397c0fb63d7a8be840b19aa9113d4.png)

# AI分析
ポーリング結果の数値をBrain.jsのAIで分析します。クリックすると分析中の

![](/images/books/twlogaian-manual/picture_pc_6c3434f7129aeeec0dcc502082ef479b.png)

のようなダイアログが表示されます。分析が終わると＜グラフと集計＞に表示できるAI分析結果のメニューが増えます。
このAIはBrain.jsを試しに使ってみた試作なので、そんなに賢くありません。過度の期待をしないでください。あなたの代わり異常を判断してくれません。Brain.jsが進化するか、他によいAIライブラリが見つかれば改善すると思います。

# AIヒートマップ
AI分析を実施した後、表示できるグラフです。

![](/images/books/twlogaian-manual/picture_pc_f521b8d3ec1681c367112f834d75c1ba.png)

日毎と時間帯別に異常スコアをヒートマップで表示しています。赤いところが異常を示しています。この例だと周期的におかしいようです。

# AI異常割合
AI分析の結果から異常と正常の割合を円グラフで表したものです。

![](/images/books/twlogaian-manual/picture_pc_bc539f135e775990c5518c54365845c0.png)

# AI時系列
AI分析の結果を時系列のグラフで表したものです。

![](/images/books/twlogaian-manual/picture_pc_7672a3c5850fccd57e020921159c11db.png)

# STL分析
ポーリング結果の数値データをSTL分析（季節性、傾向、突発の成分に分解）したグラフです。

![](/images/books/twlogaian-manual/picture_pc_dc637b3d35350f67e5956ff649219e3f.png)

# FFT分析
ポーリング結果の数値データをFFT分析（周期的な変化を周波数で分析）したグラフです。

![](/images/books/twlogaian-manual/picture_pc_86eb9595b093369c724b259470a9121c.png)

