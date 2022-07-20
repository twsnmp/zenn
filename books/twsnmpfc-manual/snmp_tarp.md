---
title: "SNMP TRAP"
---

# SNMP TRAP画面の表示方法
メニューの「ログ」ー「SNMP TRAP」をクリックすると表示できます。

![](/images/books/twsnmpfc-manual/picture_pc_21378dcaf93873c695da8f517969e741.png)

# SNMP TRAP画面

![](/images/books/twsnmpfc-manual/picture_pc_276cce53a42f678329f45ad26174d9f6.png)

のような感じです。私の環境ではあまりTRAPを受信しないのでテスト送信したTRAPだけで寂しい画面になっています。

#### ①グラフ
SNMP TRAPの受信数のグラフです。

#### ②リスト
SNMP TRAPを受信した日時、送信元、TRAPの種別、付帯しているMIBの情報のリストです。項目もクリックすると並べ替えできます。

#### ③ディスプレーフィルター
リストの内容を送信元、TRAPの種別、付帯しているMIB情報に含まれる文字列でフィルター表示できます。

#### ④＜検索条件＞ボタン
クリックするとSNMP　TRAPのログを検索するダイアログを表示します。

![](/images/books/twsnmpfc-manual/picture_pc_f7e7e1e16a7af32c06fdadf225d9d78f.png)

条件を入力して＜検索＞ボタンをクリックするとデータストアから条件にあうSNMP　TRAPのログを検索して表示します。

#### ⑤＜CSV>ボタン
SNMP TRAPログのリストをCSVファイルに保存します。

#### ⑥＜EXCEL＞ボタン
SNMP TRAPログのリストをEXCELファイルに保存します。

#### ⑦＜更新＞ボタン
前回と同じ条件でSNMP TRAPログをデータストアから検索して表示します。

