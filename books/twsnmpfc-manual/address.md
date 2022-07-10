---
title: "アドレス分析"
---

TWSNMP FCのアドレス分析画面についての説明です。私は仕事でIPアドレスやMACアドレスの情報を調べることが多いのですが、ネットで検索するのが面倒なので付けた機能です。かなり便利だと思っています。



# アドレス分析画面の表示方法
メニューの「アドレス分析」をクリックすると表示されます。

![](/images/books/twlogaian-manual/picture_pc_b2e064df30ac01e4d4e48665e91aa2aa.png)

デバイスレポートの

![](/images/books/twlogaian-manual/picture_pc_1a9d01304c90d6419da0903b170f1567.png)

操作のボタンやサーバーレポートの

![](/images/books/twlogaian-manual/picture_pc_c310edeee81ae5dcf287f3a8f7138da8.png)

操作のボタンからも調査するアドレスを指定して表示できます。

# アドレス分析画面
メニューから起動した場合は、

![](/images/books/twlogaian-manual/picture_pc_f0397e1aebed41f83986d55b9cd687d2.png)

のようにアドレスが空欄になります。このアドレスい調査したいIPアドレスかMACアドレスを入力して＜調査＞ボタンをクリックすれば、

![](/images/books/twlogaian-manual/picture_pc_c9cef3fd0e2cc0ef2fbc1ed4196ba799.png)

のように調査結果が表示されます。

#### ＜地図＞ボタン
GeoIPデータベースで位置情報が特定できた場合にこのボタンが表示されます。クリックすれば、Google Mapで地図を表示します。

![](/images/books/twlogaian-manual/picture_pc_e6efe16f7516a65e9ddc6f2a2c50bd22.png)

#### ＜CSV>ボタン
調査結果をCSVファイルに保存します。

#### ＜EXCEL＞ボタン
調査結果をEXCELファイルに保存します。

#### ＜戻る＞ボタン
この画面を表示する前の画面に戻ります。デバイスレポートから表示した場合はデバイスレポートの画面に戻ります。

# IPアドレスの場合の調査内容
主に以下の情報を表示します。

- TWSNMP FCで管理しているノードか？
- DNSで調べた名前
- GeoIPデータベースで調べた位置情報
- RDAP（Whois）で調べたアドレスの情報
- DNSブラックリストで検索したアドレスの情報

# MACアドレスの場合の調査内容

![](/images/books/twlogaian-manual/picture_pc_5b251fb7363cdca89edd7068aed91b01.png)

主に以下の情報を表示します。

- TWSNMP FCで管理しているノードか？
- MACアドレスに対応したベンダー（メーカー）
- ARP監視で調べたIPアドレス
- デバイスレポートでのIPアドレス
- デバイスレポートでの信用スコアと期間

