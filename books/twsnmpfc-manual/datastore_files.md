---
title: "データストア内のファイルと玄人向け拡張方法（プライベートMIB対応など）"
---

TWSNMP FCのデータストアフォルダに関する説明です。データストア内にあるファイルと特定のファイルを追加することで機能拡張できます。


# データベースファイル
`twsnmpfc.db`です。bboltのバイナリなので見ることはできません。停止状態でコピーすれば、バックアップできます。別のマシンにコピーできます。

# バックアップフォルダ
`backup`です。データストアのバックアップ設定

![](/images/books/twsnmpfc-manual/1658953510770-jIZ926MW6p.png)

すれば、定期的にバックアップファイルをこのフォルダに保存します。

# サーバー証明書と秘密鍵
`cert.pem`と`key.pem`です。TWSNMP FCのWeb画面をHTTPSでアクセスするためのサーバー証明書と秘密鍵です。データストアに保存しておけば、指定のファイルを利用します。存在しない状態でHTTPSモードで起動すれば自動で自己署名の証明書を作成します。

# MIBファイル
`mib.txt`というファイルをデータストアに保存すれば、組み込まれているmib.txtを置き換えます。あまり必要はないと思います。

組み込まれているファイルは、

https://github.com/twsnmp/twsnmpfc/blob/main/conf/mib.txt


です。

`mib.txt`の作り方は

https://github.com/twsnmp/go-mibdb

を見てください。

# 拡張MIBフォルダ
`extmibs`です。はじめは存在しないので必要なら作成してください。
このフォルダにASN.1形式のMIBファイルをコピーすれば、TWSNMP FCの起動時に読み込みます。エラーがあって読み込まない場合はコンソールのログに表示されます。
正しく読み込めた場合は

```
2022-07-28T05:56:12.049 load ext mib path=tmp/extmibs/jema-mib_file.txt
2022-07-28T05:56:12.066 module jemaUpsMIB=jema.1
```

のようにファイル名と認識したモジュール名が表示されます。
エラーがある場合は、

```
2022-07-28T06:00:52.624 load ext mib path=tmp/extmibs/jema-mib_file.txt
2022-07-28T06:00:52.637 21:21: unexpected "010207" (expected <extutctime> ...)
```

のようなエラーが表示されます。
正しく読み込めれば、

![](/images/books/twsnmpfc-manual/1658955913346-9XKrepaZRA.png)

のようにMIBブラウザーのMIBツリーから確認できます。

# サービスファイル
`services.txt`です。ポート番号とプロトコル名のデータベースファイルです。
組み込まれているのは

https://github.com/twsnmp/twsnmpfc/blob/main/conf/services.txt

です。変更する必要はないと思います。

# MACアドレスとベンダー名データベース
`mac-vendors-export.csv`です。MACアドレスのベンダーコードからベンダーの名前を探すデータベースファイルです。
組み込んでいるのは、

https://github.com/twsnmp/twsnmpfc/blob/main/conf/mac-vendors-export.csv


です。オリジナルは

https://maclookup.app/downloads/csv-database

です。

# 休日定義ファイル
`yasumi.txt`です。AI分析の時に休みの日を判定するために使うファイルです。
組み込まれているのは、

https://github.com/twsnmp/twsnmpfc/blob/main/conf/yasumi.txt

です。２０２２年分まであります。会社の休みに合わせて追加するとAIが賢くなるかもしれません。

# TLSの暗号名定義ファイル
`tlsparams.csv`です。TLS通信の暗号スイートの名前を定義したファイルです。組み込まれているのは

https://github.com/twsnmp/twsnmpfc/blob/main/conf/tlsparams.csv


です。変更する必要はないと思います。

# IP位置情報データベース
`geoip.mmdb`です。IPアドレスから位置情報を検索するためのデータベースファイルです。Web画面からアップロードできます。

![](/images/books/twsnmpfc-manual/picture_pc_0bc15753a622c34c760f832b7cfe0941.png)

# ポーリング定義
`polling.json`です。ポーリングの定義ファイルです。
デフォルトで組み込んでいるのは、

https://github.com/twsnmp/twsnmpfc/blob/main/conf/polling.json

です。置き換えではなく追加できます。

# ポーリングコマンドフォルダ
`cmd`です。コマンド実行のポーリング用のコマンドを保存するフォルダです。安全のためにパスを指定して実行できないようにするためにフォルダを固定しています。

# 通知メールのテンプレート
`mail_test.html`,`mail_notify.html`,`mail_report.htm`です。
通知メールのテンプレートです。変更すれば通知メールの中身をカスタマイズできます。
組み込まれているのは、

### テストメール

https://github.com/twsnmp/twsnmpfc/blob/main/conf/mail_test.html

### 通知メール

https://github.com/twsnmp/twsnmpfc/blob/main/conf/mail_notify.html


### 定期レポートメール

https://github.com/twsnmp/twsnmpfc/blob/main/conf/mail_report.html


です。

テンプレートは

https://miyahara.hikaru.dev/posts/20200313/

の記法です。

