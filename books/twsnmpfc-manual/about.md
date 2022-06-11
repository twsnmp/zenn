---
title: "TWSNMP FCではじめるネットワーク管理"
---

# TWSNMP FCとは

私は1990年代からネットワーク管理ソフトを開発してきました。
フリーソフトとして配布したWindows版のTWSNMPは2011年で開発を中止しました。
その復刻版を2019年に開発してみましたが、いまいち性能や機能の面で満足できなかったため
2021年の元日からDokcerコンテナでも使えるTWSNMP FCの開発を始めました。
自分で満足できるネットワーク管理ソフトを目指して開発しています。
きっと他の人にも役立つと思っています。



# 安全を目指すネットワーク管理

「ネットワーク管理とは？」を調べると「Open Systems Interconnection (OSI) 」のFCAPSモデルというちょっと難しい説明がでてきます。

- 障害管理(Fault Management)
- 構成管理(Configuration Management)
- 課金管理(Accounting Management)
- 性能管理(Performance Management)
- セキュリティー管理(Security Management)

の頭文字をとったモデルです。私がネットワーク管理の開発に関わり始めたころからあるものです。
簡単にいうと

- ネットワークがちゃんと使える？(F)
- ネットワーク繋がりは？（C)
- ネットワークの使用料はいくらか？(A)
- ネットワークが遅くないか？(P)
- ネットワークが安全か？(S)

という質問に答えることだと思います。
TWSNMPも真面目にこのモデルを実現しようと考えて作ってきました。
オリジナルのTWSNMPを開発したころの重要性は

F > P > C > A > S

だったと思います。今（2021年）は、

S >> C > F > P  >> A

のような感じだと思っています。
最近のネットワーク機器やサーバーは高性能で高信頼なので故障や性能の問題は起こりにくくなっています。
ネットワークの利用料金も定額なので気にする必要がなくなっています。
それに比べてセキュリティーの重要度が大きくなっています。
悲しいことにインターネットを利用して悪いことをする人が増えたことが原因です。

このようなことを考えてTWSNMP FCでは、オリジナルのTWSNMPよりもセキュリティー管理のための機能を充実しようとしています。
TWSNMP FCでネットワークを調べてクリーンなネットワークを作れるか試しています。

## 障害管理(F)

TWSNMP FCで各種ポーリングによってネットワーク上で発生する障害を知ることができます。

![](/images/books/twsnmpfc-manual/2022-06-08_13-26-53.png)

## 構成管理（C)

TWSNMP FCでネットワークの構成をマップに表示することができます。

![](/images/books/twsnmpfc-manual/picture_pc_fa9a0b086ac208315e40218c93e3327e.png)

## 性能管理（P)

TWSNMP FCでポーリングの結果から性能に関する情報を知ることができます。

![](/images/books/twsnmpfc-manual/picture_pc_daaf8efc029f65d14aacc569d86db367.png)

## セキュリティー管理(S)

TWSNMP FCはセキュリティー管理に最も力をいれています。レポート機能では

- どんなデバイスがネットワークに接続されているか？
- そのデバイスは、どんなサーバーと通信しているのか？
- 何の目的で通信しているのか？
- 通信している相手が何処の地域（国、都市）のサーバーか？
- 暗号通信の強度に問題ないか？
- サーバーの証明書に問題ないか？

を調べられるようになっています。そして、その利用方法は他と比べて安全なのかを信用スコアで示すようになっています。

例えば、LAN上のデバイスは、

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_cf9bb377525080c255d957285516577d.png)

のようなデバイスをリストアップするレポートで調べることができます。
知らないうちに接続された機器を発見できるかもしれません。


オムロンの環境センサーを設置すれば、

![](/images/books/twsnmpfc-manual/picture_pc_f76eaa9f28197c2f71935340bca220b7.png)

のような環境に関するレポートも作成できます。


ユーザーがサーバーへログインしている状況は

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_3e14303fea22729103e816966574d159.png)

のようなレポートで確認できます。ログインに失敗が多いユーザーを見つけることもできます。

サーバーの証明書を

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_afacea1c15abd6438a04c78effd32428.png)

のようなレポートで管理することができます。期限切れでアクセスに問題が発生すること
を未然に防げると思います。


管理対象のネットワーク内の暗号通信（TLS）の安全性は

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_ac443643407ae4a65f24380ffbc2a66f.png)

のようなレポートで確認できます。TLSの暗号強度を一覧表示してくれます。

管理対象のネットワークからアクセスしているサーバーは

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_e302eaf1290e21dfc52c3896fc241097.png)

のレポートで確認できます。アクセス先のサーバーが設置されている国を知ることもできます。


管理対象のネットワークで使われているIPアドレスは


![](/images/books/twsnmpfc-manual/rectangle_large_type_2_53efa9be2998171ffc5f97db8e619176.png)


のようなレポートで確認することができます。IPアドレスの一覧表を作成することも簡単です。


管理対象のネットワーク上のIPv4とIPv6の割合は

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_53efa9be2998171ffc5f97db8e619176.png)

のEthernetフレームタイプのレポートで知ることができます。


Windowsのイベントログの集計リストは

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_34d6d7f5d9f1efa850633d4af0e7d045.png)

で調べることができます。

他にも沢山のレポートがあります。これからも増えていくと思います。

# 他のコンテナやセンサーによるチームプレー

ネットワークの障害や構成を管理するだけならオリジナルのTWSNMPのように単体のソフトだけで必要な機能を満たすことができますが、
セキュリティーに重点をおくと情報収集のために他のソフトや機材の助けが必要です。
TWSNMP FCは他のコンテナと連携するチームプレーでネットワーク管理を実現することが可能です。
TWSNMP FCのパッケージにはセンサープログラム含まれています。

![](/images/books/twsnmpfc-manual/rectangle_large_type_2_8d0a2f2a294c69f41b6b3dd9a53cdac8.png)


# 機能改善のスピードアップ

オリジナルのTWSNMPや復刻版のTWSNMPのようにインストラーで配布するデスクトップアプリケーションだと機能の追加や改善した後、配布や入れ替えに厄介な作業が発生します。これでは良いアイデアを試すのが嫌になってしまいます。
そこでTWSNMP FCではDockerコンテナ版を主な配布方法にしています。
コンテナ版のlatestは[noteの開発日誌](https://note.com/twsnmp/m/m51b45353e2ff)の内容が常に反映された状態になっています。

# AI分析

沢山のノードやポーリングを登録すると人間がリストやグラフを見て問題を判断するのはかなり大変です。
できるだけコンピューターの力で自動判断できたほうがよいので機械学習による異常判断を組み込んでいます。


![](/images/books/twsnmpfc-manual/rectangle_large_type_2_e85e0ea03a10e899ae3c0f510bbe1acd.png)


