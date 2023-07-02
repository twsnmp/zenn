---
title: "はじめてのTWLogAIAN"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["syslog","アクセスログ","ログ分析","twsnmp","ホワイトハッカー"]
published: true
---

# はじめに

便利なAIアシスト付きログ分析ツールTWLogAIANをインストールして使い始めるまでの説明です。
TWLogAIANはソフトウェアの開発やサポートを行っている人のためのログ分析ツールです。
「ログを簡単に集めて、検索が楽になるインデックスを作成し、検索結果をリッチな表現で分析でき、終わったら簡単に片付ける」という考えで作っています。

TWLogAIANの仕組みは

![](/images/twlogaian-startup-guide/2022-05-19_04-08-41.png)

のような感じです。
全文検索エンジンにログを読み込んで検索できるようになっています。
検索結果を機械学習(AI)や可視化によって分析を助けてくれます。

# 動画マニュアル

動画でだいたいの使い方を説明しています。

https://youtu.be/XiNhuSlLYLw


注意：__猫の世界にはダークサイドはないのでホワイトハッカーしかいません。__
# インストール

## Windows版のインストール

Windows環境では、v1.5.0以降Microsoft Storeでからインストールできます。

https://ms-windows-store//pdp/?productid=9P8TQLG999Z3

からインストールしてください。

![](/images/twlogaian-startup-guide/2022-05-19_04-26-38.png)

Microsoft Storeの使えないWindows Serverには、

https://github.com/twsnmp/TWLogAIAN/releases

からWindows版のMSI形式のインストラーTWLogAIAN.msiをダウンロードしてインストールすることもできます。
この方法は、
https://note.com/twsnmp/n/n81b59b61c56e?magazine_key=m9c88e79743b6
にあります。

## Windows版をScoopからインストール

Windows版はScoopのtwsnmp Bucketで公開しています。(v1.25.0から)

### Scoopのインストール

Scoopのサイト

https://scoop.sh/

に記載の方法で

```
>Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
>irm get.scoop.sh | iex
```

でScoopをPowerShellからインストールします。

### TWLogAIANのインストール

```
>scoop bucket add twsnmp https://github.com/twsnmp/scoop-bucket
>scoop install twlogaian
```

でインストールできます。
Microsoft StoreやMSIからインストールした場合との違いは、
実行ファイルにPATHが通っていることです。
アップデートもできます。

コマンドラインから

```
>TWLogAIAN.exe
```

のように指定して起動できます。


## Mac OS版のインストール

v1.7.0以降は、Mac OS版もApple App Storeで公開しています。

![](/images/books/twlogaian-manual/2023-01-21_15-51-47.png)


ストアのリンクは
https://apps.apple.com/app/twlogaian/id1664596440

です。こちらからインストールしてください。


# TWLogAIANの起動

Windowsの場合はスタートメニューからMac OSの場合はランチャーからなどお好きな方法で起動してください。
ようこそ画面が表示されるはずです。

![](/images/books/twlogaian-manual/2023-01-21_15-56-31.png)

右上の🌙マークをクリックすれば、ダークモードになります。

![](/images/books/twlogaian-manual/2023-01-21_15-57-05.png)

私はダークモードが好きです。たぶんホワイトハッカーの目指す人はダークモードが好きだと思います。

v1.7.0から右上のメニューで画面の表示を英語に切り替えられます。

![](/images/books/twlogaian-manual/2023-01-21_15-58-07.png)

# TWLogAIANによる分析の流れ

## 作業フォルダの選択

＜分析をはじめる＞ボタンをクリックすると、作業フォルダの選択画面が表示されます。

![](/images/twlogaian-startup-guide/2022-05-19_04-42-41.png)

作業フォルダーには分析のための設定ファイルと全文検索エンジンのインデックスが作成されます。
分析が終わったらフォルダーごと削除すれば全部消えます。証拠隠滅できます。

## ログの読み込み場所の設定

作業フォルダーを選択するとログ分析の設定画面が表示されます。
最初に、ログを読み込む場所の設定をします。分析対象のログが何処にあるかを設定します。
最初は＜＋＞ボタンで追加できます。
沢山種類がありますが、簡単なのは、単一のファイルかローカルのフォルダです。
フォルダを指定するとファイル名のパターンを指定して対象を限定することがきます。

![](/images/twlogaian-startup-guide/2022-05-19_04-45-22.png)

この例だと指定のフォルダにあるファイル名がaccessから始まるもの対象です。

## ログの読み込み処理の設定

対象のログを読み込む場所を指定したら読み込む時の処理の設定です。

![](/images/books/twlogaian-manual/2023-01-21_16-05-19.png)

圧縮ファイルの中の圧縮ファイルの扱いやタイムゾーンがない場合の時刻の扱い、
読み込むログをフィルターで制限する設定、ログの中からデータを抽出するための設定、
IPアドレスなどの情報からホスト名や位置情報を調べる設定、
インデックスの作成場所に関する設定があります。

詳しくは別の記事で解説します。最初は適当に設定してみてください。

## ログの読み込み

＜インデックス作成＞ボタンをクリックするとログの読み込みを開始します。
読み込み中は進行状況を表示します。

![](/images/books/twlogaian-manual/2023-01-21_16-37-31.png)

## ログの検索

ログを読み込んでインデックスの作成が完了すると検索画面が表示されます。
とりあえず＜検索＞ボタンをクリックすれば

![](/images/books/twlogaian-manual/2023-01-21_16-39-35.png)

のように検索できます。

ログの読み込みの状況は、＜処理結果＞ボタンで確認できます。

![](/images/books/twlogaian-manual/2023-01-22_05-50-35.png)

検索条件を指定して検索することもできます。

![](/images/books/twlogaian-manual/2023-01-21_16-42-25.png)

時間範囲や位置情報、

IPアドレスから位置情報を抽出する設定にすれば、

![](/images/books/twlogaian-manual/2023-01-21_17-45-57.png)

のようなレポートも表示できます。
 
 それでは快適なログ分析ライフをお楽しみください。
