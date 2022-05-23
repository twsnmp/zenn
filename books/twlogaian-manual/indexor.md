---
title: "インデックス作成の流れ"
---


TWLogAIANはログファイルを読み込んで全文検索エンジンのインデックスを作成をします。
インデックス作成するための流れについて説明します。

![](/images/books/twlogaian-manual/2022-05-24_05-09-01.png)

の赤枠の部分の説明です。

ログを読み込んだら行単位で意味のなる情報を抽出してインデックスに登録します。例えば、

```
114.119.136.254 - - [03/Apr/2022:00:39:21 +0900] "GET /wiki/index.php?title=Must_Know_Mlm_Concepts_For_Accomplishment&action=history HTTP/1.1" 404 1417 "-" "Mozilla/5.0 (Linux; Android 7.0;) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36 (compatible; PetalBot;+https://webmaster.petalsearch.com/site/petalbot)"
```

のようなApacheのアクセスログの場合、クライアントのIPアドレス、時刻、リクエスト、パスなどの情報があります。
この行をまとめて全文検索エンジンに登録することもできますが、
各項目を抽出してインデックスの項目（フィールド）として登録したほうが検索する時に役に立ちます。
検索が早くなるととか集計しやすいとかです。

この例をApache(Combined)のタイプとして処理すると

![](/images/books/twlogaian-manual/2022-05-24_05-04-41.png)

のような項目を抽出します。
この例ではログに書かれている内容から取得したものとクライアントのIPからDNSでホスト名を調べたり、
位置情報を調べたりして項目を追加しています。
TWLogAIANはログ分析ツールなので、最低タイムスタンプは抽出します。
世の中で使われているログの形式に関しては組み込んであります。カスタム設定で自分で抽出項目を選ぶこともできます。



