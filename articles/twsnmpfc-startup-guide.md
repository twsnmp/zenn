---
title: "はじめてのTWSNMP FC"
emoji: "🖥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["twsnmp","snmp","netflow","syslog","ping"]
published: true
---
# はじめに

この記事はTWSNMP FCをインストールして使い始めるまでの説明です。
TWSNMP FCは20年以上前に作ったSNMPv3対応のネットワーク管理ソフト
TWSNMPマネージャを2021年の最新技術でリニューアルしたソフトです。
Windows/Mac OS/Linuxで動作しますが一番オススメの環境はLinux上のDocker環境です。
Docker版の場合は常に最新のバージョンを利用できます。
リリース版は少し遅れて配布しています。
WindowsやMac OSのDocker Desktop環境だとネットワーク環境の問題で
ARP監視やデバイスレポートに制限があります。

# Windows版のインスール

Windows版は、Microsoft Storeに公開しています。(v.1.11.0から）

https://www.microsoft.com/store/apps/9NN1DG80K76M



Microsoft Storeから直接インストールできます。

![](/images/twsnmpfc-startup-guide/1652299365939-kOn9ypqOW9.png)

Server OSなどにインストールしたい場合はMSI形式のインストラーも用意
しています。

# インストラーのダウンロード

リリース版はGitHubのリポジトリからダウンロードできます。
最新のリリースは、

https://github.com/twsnmp/twsnmpfc/releases

で公開しています。

![](/images/twsnmpfc-startup-guide/picture_pc_474cc557ed41c920d1e2436cc613ec07.png)

ダウンロードしたらHASH値を確認することをオススメします。
Mac OS版はdmgファイル、Windows版はmsiファイル、Linux版はdebファイルのインストラーがあります。
これらは署名してあります。
Windowsのmsiファイルや実行ファイルの署名を検証するためには

https://lhx98.linkclub.jp/twise.co.jp/download/twsnmp.cer

の証明書をインポートしてください。

ZIPファイルは署名なしの実行ファイルが実行ファイルが一つだけあります。
お好きなフォルダに解凍してください。

# Mac OS版のインストール

ダウンロードしたtwsnmp.dmgファイルをダブルクリックすれば、

![](/images/twsnmpfc-startup-guide/2022-05-15_07-32-58.png)

のような使用許諾が表示されます。＜同意します＞をクリックすれば、

![](/images/twsnmpfc-startup-guide/2022-05-15_07-33-23.png)

ドラック＆ドロップでインストールできます。

# Linux版のインストール

DebianまたはUbuntuの場合は、aptコマンドでインストールできます。
Rasiberry  Piも同じ方法でできます。
まず、公開鍵をインポートしてください。root権限がsudoで実行してください。

```bash
wget -O -  https://lhx98.linkclub.jp/twise.co.jp/download/twsnmp.gpg.key |  apt-key add -
```

OKと表示されたらインポートできています。

```
E: gnupg, gnupg2 and gnupg1 do not seem to be installed, but one of them is required for this operation
```

のようなエラーがでたら、

```shell
apt-get update && apt-get install -y gnupg2
```

を実行してください。
/etc/apt/source.listに

```
deb https://lhx98.linkclub.jp/twise.co.jp/debian bulleseye main
```

の行を追加してください。

```shell
apt update
apt install twsnmpfc
```

を実行すればインストールできます。
他のディストリビューションのLinux環境ではzipファイルをダウンロードして
/opt/twsnmpfcなどに解凍してインストールして下さい。

# Windows/Mac OS版の起動ツール（GUI）からの起動方法

v1.7.0から起動ツールが付属しています。
Windowsの場合は、「スタート」ー「TWSNMP FC」ー「TWSNMP起動ツール」

![](/images/twsnmpfc-startup-guide/2022-05-15_07-49-51.png)

をクリックしてください。
Mac OSの場合は、twLaucherを起動してください。

![](/images/twsnmpfc-startup-guide/2022-05-15_07-52-17.png)


WindowのTWSNMP FCの起動は

![](/images/twsnmpfc-startup-guide/2022-05-15_07-54-30.png)


のような感じです。
Mac OSは

![](/images/twsnmpfc-startup-guide/2022-05-15_07-54-38.png)

です。

どちらのOSでも起動は３ステップです。

1. データストアのフォルダを選択する

2. 外部からのアクセスを許可しない場合はローカルをチェック、Windowsでタスクスケジューラーに登録する場合はスケジューラーにチェック

3. ＜起動＞ボタンをクリック

＜起動＞ボタンが＜停止＞ボタンに変われば起動できています。
エラーの場合にはメッセージが表示されます。
センサープログラムもこの起動ツールから起動できます。
必要なパラメータを入力して起動ボタンをクリックするだけです。

 
# Linux/Mac OS/Windowsでのコマンドラインからの起動方法

実行ファイルを解凍したフォルダでデータストア用のフォルダを作成して起動すれば、すぐ使えます。

```bash
mkdir datastore
twsnmpfc.app --local
```

パラメータに--localをつけるとループバックアドレスのポートだけをオープンして起動します。
起動後にブラウザーの画面も自動で表示します。
--localを付けないと他のパソコンからもアクセス可能な状態になるので注意してください。

起動のパラメータは、

```
% ./twsnmpfc.app -h
Usage of ./twsnmpfc.app:
 -cpuprofile file
   	write cpu profile to file
 -datastore string
   	Path to Data Store directory (default "./datastore")
 -host string
   	Host Name for TLS Cert
 -ip string
   	IP Address for TLS Cert
 -local
   	Local only
 -memprofile file
   	write memory profile to file
 -password string
   	Master Password (default "twsnmpfc!")
 -ping string
   	ping mode icmp or udp
 -port string
   	port (default "8080")
 -restore string
   	Restore DB file name
 -tls
   	Use TLS
```

です。

Windowsの場合はデフォルトで

C:\Program Files\TWSNMP FC\twsnmpfc.exe
にインストールされます。PATHなどを設定するかフルパスでコマンドを実行してください。
Linuxでパッケージからインストールした場合は、

/opt/twsnmpfc

にインストールされます。


-cpuprofile と-memprofile はデバック用なので開発しない人は気にしないでください。
-datastoreはデータを保存するディレクトリです。デフォルは"./datastore"です。
-host と-ip はブラウザーからの接続をhttps(暗号化)にするためのサーバー証明書を作るための情報です。わからない場合は気にしないでください。

-localはTWSNMP FCを起動したパソコンからだけアクセス可能にしてブラウザーも自動で起動してくれます。
-passwordはTWSNMP FC内部で使用しているマスターキーのようなものです。同じ設定だと危ないので他のパソコンからもアクセスできるようにする場合は変えてください。
-portはブラウザーからアクセスするポート番号です。デフォルト "8080"です。
-tlsはhttpsでアクセスできるようにするための設定です。
サーバー証明書が必要ですなければ自動生成します。
-pingはPINGのモードを指定します。icmpかudpを指定できます。
Dockerも含めてLinux環境でpingのモードをudpを指定した場合、
以下のコマンドを実行しないとPINGが機能しません。
v1.5.0以降のバージョンはデフォルトでpingモードをicmpです。

```shell
sudo sysctl -w net.ipv4.ping_group_range="0 65535"
```

# Docker環境での起動方法

Docker環境では実行ファイルをダウンロードする必要はありません。Docker Hubで公開しています。

https://hub.docker.com/repository/docker/twsnmp/twsnmpfc


Linux環境でpingモードをudpで利用する時は、少し前に書いたPINGのための設定を実行しておいてください。

以下のコマンドでTWSNMP FCを起動できます。

```shell
docker  volume create twsnmpfc 
docker  run --rm -d --net host -v twsnmpfc:/datastore twsnmp/twsnmpfc
```

WindowsやMac OSのデスクトップ版Docker環境の場合は、

```shell
docker  volume create twsnmpfc 
docker  run  --rm -d --sysctl net.ipv4.ping_group_range="0 65535" -p 8080:8080 -v twsnmpfc:/datastore  twsnmp/twsnmpfc
```

のように起動します。この場合、ARP監視やデバイスレポートの動作に制限があります。

```
--sysctl net.ipv4.ping_group_range="0 65535"
```

はPINGをUDPモードにした時だけ必要です。


# ブラウザーからアクセス

起動できたらブラウザーから

```
http://<TWSNMP FCのIP>:8080/
※8080はデフォルトのポート番号、変更した場合は合わせてください。
```

にアクセスすると

![](/images/twsnmpfc-startup-guide/2022-05-15_08-10-59.png)

のような画面が表示されるはずです。

＜ログイン＞ボタンをクリックすれば

![](/images/twsnmpfc-startup-guide/2022-05-15_08-14-35.png)

の画面が表示されます。

ユーザーID、パスワードの初期値は、

```
ユーザーID：twsnmp
パスワード：twsnmp
```

です。ログインしたら空のマップが表示されます。

「システム設定」ー「マップ」メニューからマップ設定をクリックします。

![](/images/twsnmpfc-startup-guide/2022-05-15_08-17-43.png)

マップ名、ユーザーID、パスワードを変更してください。
その他マップ名などの必要な項目を変更してください。

設定できたら「自動発見」メニューから自動発見画面

![](/images/twsnmpfc-startup-guide/2022-05-15_08-20-04.png)

で管理したいネットワークのIPアドレス範囲を指定して＜開始＞ボタンを
クリックしてください。

**※アクティブモードで自動発見を実施するとパソコンにインストールしたセキュリティーソフトなどがポートスキャンを検知したという警告を表示する場合があるので検索する範囲は十分注意してください。**

完了すればマップ上にノードが表示されます。


![](/images/twsnmpfc-startup-guide/2022-05-15_08-26-17.png)


マップ上のアイコンをドラッグすれば移動できます。複数選択しての移動もできます。SHITキーを押しながら２つのノードを選択すればラインの接続もできます。自分の好みに合わせてマップを編集してみてください。

# センサープログラムについて

Windows,Mac OS,Linuxのパッケージからインストールすると各種センサープログラムもインストールされます。

センサープログラムの説明は

https://note.com/twsnmp/n/nba97c75b0efc


をみてください。(いずれ、Zennにも書きます)

