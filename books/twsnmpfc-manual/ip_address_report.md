---
title: "IPアドレスレポート"
---

TWSNMP FCのIPアドレスレポートについての説明です。TWSNMP FCはARP Watch、NetFlow、twpcapセンサーなどのsyslogからIPアドレスを見つけてサポートを作成します。管理対象のネットワークの通信で使われているIPアドレスのリストです。IPv6のアドレスはIPFIXかtwpcapでしか検知できません。IPv6アドレスを検知できるようにすると以外なほど沢山でてきて驚くと思います。


# IPアドレスレポートの表示方法
メニューの「レポート」ー「NetFlow分析」ー「IPアドレス」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_0c86b24587d26ffbf0882cda185faf39.png)

# IPアドレスレポート画面

![](/images/books/twsnmpfc-manual/picture_pc_dd277a893e66aecd6041198fd3fcd60f.png)

のような感じです。

#### ①IPアドレスリスト
TWSNMP FCで見つけたIPアドレスのリストです。信用スコア、IPアドレス、名前（ホスト名か登録名）、国、MACアドレス、ベンダー、初回検知日時、最終検知日時、操作ボタンがあります。国はIPアドレスから位置情報が取得できる場合に表示されます。MACアドレス、ベンダーはMACアドレスがわかる場合に表示されます。MACアドレスは、ARPテーブルやtwpcapのログから取得する方法とIPv6アドレスにMACアドレスが含まれる場合に取得できます。

#### ②操作ボタン

![](/images/books/twsnmpfc-manual/picture_pc_d0e5f319216f93b218dec0ad25ce4756.png)

左から＜マップ＞ボタン、＜IPアドレス分析＞ボタン、＜MACアドレス分析＞ボタン、＜詳細＞ボタン、＜削除＞ボタンです。
＜マップ＞ボタンはIPアドレスが管理マップに登録されているノードの場合に表示されます。
＜IPアドレス分析＞＜MACアドレス分析＞ボタンをクリックするとアドレス分析で選択したIPアドレスまたはMACアドレスの調査を行います。
＜詳細＞ボタンをクリックするとIPアドレスに関する詳細情報を表示します。
＜削除＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_3359a2bdeb40ff963c3ca8ca50b524d8.png)

の確認ダイアログを表示します。＜削除＞をクリックするとレポートから削除できます。

#### ③ディスプレーフィルター
リストの内容をIPアドレス、名前、国、MACアドレス、ベンダーに入力した文字列を含むものでフィルター表示します。＜条件を反転＞をオンにすると入力した文字列を含まないものになります。IPアドレスに:を入力すれば、IPｖ６だけになります。この状態で＜条件を判定＞をオンにすればIPv4だけになります。

#### ④グラフと集計
グラフと集計のメニューを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_2e65b907f036f2ac8f6aa0e5efc3f858.png)

#### ⑤＜CSV>ボタン
IPアドレスリストの内容をCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
IPアドレスリストの内容をEXCELファイルに保存します。

#### ⑦＜再計算＞ボタン
クリックすると

![](/images/books/twsnmpfc-manual/picture_pc_99928241a967bedfb91cf1976386525d.png)

のような確認のダイアログを表示します。＜実行＞ボタンをクリックすると信用スコアを再計算します。信用スコアは数分毎に計算していますが、計算を早めるためのボタンです。

##### ⑧＜更新＞ボタン
IPアドレスリストの内容を最新の情報に更新します。

# IPアドレス詳細画面

![](/images/books/twsnmpfc-manual/picture_pc_6b1393e301d7816218c24421d30c9e56.png)

のような感じです。IPアドレス、MACアドレス欄にはコピーボタンがあります。アドレスをクリップボードにコピーできます。
＜マップに追加＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_e6b425468133c708a486a5b0dd23bf9e.png)

のノード編集のダイアログを表示します。設定を入力して＜保存＞をクリックすればマップに管理対象ノードとして追加できます。
＜削除＞ボタンはIPアドレスを削除するためのものです。

# メーカー別集計
グラフと集計の＜メーカー別＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_d6be306fed6a5562ce0a8d8cbe8e9620.png)

のようにメーカー別に集計したグラフを表示します。

# IP位置
グラフと集計の＜IP位置＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_f4d5c23b3cb1eb913ad5a5adae8ba6cd.png)

のようにIPアドレスから位置情報が取得できるものを世界地図上に表示します。

# 国別
グラフと集計の＜国別＞ボタンをクリックすると

![](/images/books/twsnmpfc-manual/picture_pc_aaf72473726f8b0062723d287c393008.png)

のようにIPアドレスから位置情報がわかるものを国別に集計したグラフを表示します。

# IPアドレスレポートを表示するためには？
IPアドレスレポートの情報はARP Watch,NetFlow,IPFIX,twpcapセンサーのデータが必要です。NetFlowのデータはNetFlowに対応したネットワーク機器（Firewall/SW-HUBなど）かLinuxにsoftflowdをインストールしてNetFlowのデータを送信する方法もあります。

https://hub.docker.com/r/twsnmp/softflowd
が便利です。

ARP Watchはマップ設定でオンにできます。
twpcapセンサーに関してもは別の記事で書きます。

# レポートの設定
IPアドレスレポートの信用スコアやレポートに表示するIPアドレスに関してはレポート設定画面で設定できます。
特に、

![](/images/books/twsnmpfc-manual/2022-07-18_05-25-39.png)

***MACアドレスが不明のIPもレポートに含める***

をオンにするとIPアドレスレポートに沢山登録されるようになると思います。


