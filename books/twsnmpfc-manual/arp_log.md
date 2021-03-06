---
title: "ARPログ"
---

TWSNMP FCでARPをモニターした場合のログを表示する画面の説明です。
ARPのモニターはIPアドレスに対応するMACアドレスを調べるものです。


# ARPログ画面の表示方法
メニューの「ログ」ー「ARPログ」をクリックします。

![](/images/books/twsnmpfc-manual/picture_pc_405881c0f87a8b14b16dba1e564ef1bc.png)

# ARPログ画面

![](/images/books/twsnmpfc-manual/picture_pc_abc90bc061fe9b97e53b230f28838431.png)

のような感じです。

#### ①グラフ
ログの記録状況を示すグラフです。

#### ②リスト
状態、発生日時、IPアドレス、MACアドレス、ベンダー、変化前のMACアドレス、変化前のベンダーのリストです。項目をクリックすると並べ替えできます。
状態としては、新規発見と変化があります。この画面のように、同じIPアドレスで変化が繰り返し発生していのは、同じセグメントに２つのLANポートで接続しているノードがあるためです。ネットワークキャプチャー用のポートを接続しています。

#### ③ディスプレーフィルター
状態は選択式です。IPアドレス、MACアドレス、ベンダー、変化前のMACアドレス、変化前のベンダーは入力した文字列を含む項目をフィルター表示できます。

#### ④検索条件
クリックすると

![](/images/books/twsnmpfc-manual/picture_pc_423293877060b911b845967e045552c4.png)

のような検索条件を指定するダイアログを表示します。
期間やIPアドレス、MACアドレスを指定して検索できます。

#### ⑤＜CSV>ボタン
リストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
リストの内容をEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
前回と同じ条件で検索を行いリストを更新します。

# ARPログを記録する方法
マップ設定でARP Watchをオンにします。

![](/images/books/twsnmpfc-manual/picture_pc_288f30658bec481e29cc5e1c6838cc97.png)

