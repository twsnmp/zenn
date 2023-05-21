---
title: "インストールと起動方法"
---

TWSNMP FCをインストールする方法の説明です。

# Windows版をMicrosoft Storeからインストール

Windows版は、Microsoft Storeに公開しています。(v.1.11.0から）

https://www.microsoft.com/store/apps/9NN1DG80K76M


![](/images/books/twsnmpfc-manual/1652299365939-kOn9ypqOW9.png)

Microsoft StoreからのインストールのほうがMicrosoftが署名したインストラーなので
安全です。
Windows Serverにインストールしたい人はリリース版をダウンロード
していただく方法があります。

# Windows版をScoopからインストール

Windows版はScoopのtwsnmp Bucketで公開しています。(v1.25.0から)

## Scoopのインストール

Scoopのサイト

https://scoop.sh/

に記載の方法で

```
>Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
>irm get.scoop.sh | iex
```

でScoopをPowerShellからインストールします。

## TWSNMP FCのインストール

```
>scoop bucket add twsnmp https://github.com/twsnmp/scoop-bucket
>scoop install twsnmpfc
```

でインストールできます。
Microsoft StoreやMSIからインストールした場合との違いは、
実行ファイルにPATHが通っていることです。

コマンドラインから

```
>twsnmpfc.exe -datastore c:\twsnmpfc -local
```

のように指定して起動できます。起動ツールやセンサーも起動できます。
インストールされるセンサーは

- twWifiScan.exe: 無線APセンサー
- twWinlog.exe:Windowsイベントログセンサー
- twpcap.exe:パケットキャプチャーセンサー

です。これらをコマンドラインから起動できます。


# リリース版のダウンロード

TWSNMP FCのリリース版を

https://github.com/twsnmp/twsnmpfc/releases

で配布しています。最新のリリースからダウンロードしてください。

![](/images/books/twsnmpfc-manual/picture_pc_474cc557ed41c920d1e2436cc613ec07.png)

ダウンロードしたらHASH値を確認することをオススメします。
Mac OS版はdmgファイル、Windows版はmsiファイル、Linux版はdebファイルのインストラーがあります。
これらは署名してあります。ZIPファイルは署名なしの実行ファイルが実行ファイルが一つだけあります。
お好きなフォルダに解凍してください。

# Mac OS版のインストール

ダウンロードしたtwsnmp.dmgファイルをダブルクリックすれば、

![](/images/books/twsnmpfc-manual/1652596829795-bvX8P5LUzg.png)

のような使用許諾が表示されます。＜同意します＞をクリックすれば、

![](/images/books/twsnmpfc-manual/1652596865350-FzfePwp8D6.png)


のような画面が表示されます。
twLauncherをApplicationsにドラック＆ドロップすればインストールできます。

# Linux版のインストール

DebianまたはUbuntuの場合は、aptコマンドでインストールできます。
Rasiberry  Piも同じ方法でできます。

まず、公開鍵をインポートしてください。root権限かsudoで実行してください。

```sh
wget -O -  https://lhx98.linkclub.jp/twise.co.jp/download/twsnmp.gpg.key |  apt-key add -
```

OKと表示されたらインポートできています。

```
E: gnupg, gnupg2 and gnupg1 do not seem to be installed, but one of them is required for this operation
```

のようなエラーがでたら、

```sh
apt-get update && apt-get install -y gnupg2
```

を実行してください。

/etc/apt/source.listに

```
deb https://lhx98.linkclub.jp/twise.co.jp/debian bulleseye main
```

の行を追加してください。

```sh
apt update
apt install twsnmpfc
```

を実行すればインストールできます。

他のディストリビューションのLinux環境ではzipファイルをダウンロードして

/opt/twsnmpfcなどに解凍してインストールして下さい。

# Windows/Mac OS版の起動ツール（GUI）からの起動方法

v1.7.0から起動ツールが付属しています。
Windowsの場合は、「スタート」ー「TWSNMP FC」ー「TWSNMP起動ツール」

![](/images/books/twsnmpfc-manual/1652596978520-B75EirBnAa.png)

をクリックしてください。

:::message alert
タスクスケジューラーに登録したり、TWPCAPなどのセンサーのLAN I/F欄の情報を
表示させるためにはメニューを右クリックして管理者権限で起動してください。
:::


![](/images/books/twsnmpfc-manual/2022-06-29_06-01-50.png)

Mac OSの場合は、twLaucherを起動してください。

![](/images/books/twsnmpfc-manual/1652597005999-RAhsNoVvPT.png)


Window版のTWSNMP起動/設定ツールは

![](/images/books/twsnmpfc-manual/1641179213980-p784VzLSlh.png)

のような感じです。(v1.24.0まで)
v1.25.0からは

![](/images/books/twsnmpfc-manual/2023-05-21_05-19-12.png)

起動画面は
![](/images/books/twsnmpfc-manual/2023-05-21_05-19-28.png)

です。

Mac OS版は

![](/images/books/twsnmpfc-manual/1641179260039-gPNQ4UUSWJ.png)

です。(v.24.0まで)

v1.25.0からは
![](/images/books/twsnmpfc-manual/2023-05-22_05-58-41.png)

起動画面は

![](/images/books/twsnmpfc-manual/2023-05-22_05-57-34.png)

です。

どちらのOSでも一番簡単な起動は３ステップです。
（v1.25.0以降はリストの右下の＜＋＞ボタンから起動するプログラムを選択してください。）

1. データストアのフォルダを選択する
2. 外部からのアクセスを許可しない場合はローカルをチェック、Windowsでタスクスケジューラーに登録する場合はスケジューラーにチェック
3. ＜起動＞ボタンをクリック


＜起動＞ボタンが＜停止＞ボタンに変われば起動できています。エラーの場合にはメッセージが表示されます。
センサープログラムもこの起動ツールから起動できます。必要なパラメータを入力して起動ボタンをクリックするだけです。

Windowsのタスクスケジューラーに登録した場合は、

![](/images/books/twsnmpfc-manual/1641179584994-oKVcuy1n95.png)

のようにTWSNMPのフォルダに登録されます。

:::message alert
タスクスケジューラーに登録するためには管理者権限での実行が必要です。
:::


# Linux/Mac OS/Windowsでのコマンドラインからの起動方法

実行ファイルを解凍したフォルダでデータストア用のフォルダを作成して起動すれば、すぐ使えます。

```sh
mkdir datastore
twsnmpfc.app --local
```

パラメータに--localをつけるとループバックアドレスのポートだけをオープンして起動します。起動後にブラウザーの画面も自動で表示します。--localを付けないと他のパソコンからもアクセス可能な状態になるので注意してください。起動のパラメータは、

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
-datastoreはデータを保存するディレクトリです。デフォルは"./datastore"です。-host と-ip はブラウザーからの接続をhttps(暗号化)にするためのサーバー証明書を作るための情報です。込み入った話なので別の記事に書きます。わからない場合は気にしないでください。
-localはTWSNMP FCを起動したパソコンからだけアクセス可能にしてブラウザーも自動で起動してくれます。
-passwordはTWSNMP FC内部で使用しているマスターキーのようなものです。同じ設定だと危ないので他のパソコンからもアクセスできるようにする場合は変えてください。
-portはブラウザーからアクセスするポート番号です。デフォルト "8080"です。
-tlsはhttpsでアクセスできるようにするための設定です。サーバー証明書が必要ですなければ自動生成します。この話も込み入っているので別の記事で書きます。
-pingはPINGのモードを指定します。icmpかudpを指定できます。

# Linux環境でPINGのための設定

Dockerも含めてLinux環境でpingのモードをudpを指定した場合、以下のコマンドを実行しないとPINGが機能しません。
v1.5.0以降のバージョンはデフォルトでpingモードをicmpにしたためこの指定は必要ありません。

```sh
sudo sysctl -w net.ipv4.ping_group_range="0 65535"
```

# Docker環境での起動方法

Docker環境では実行ファイルをダウンロードする必要はありません。Docker Hubで公開しています。

https://hub.docker.com/repository/docker/twsnmp/twsnmpfc


Linux環境でpingモードをudpで利用する時は少し前に書いたPINGのための設定を実行しておいてください。
以下のコマンドでTWSNMP FCを起動できます。

```sh
docker  volume create twsnmpfc 
docker  run --rm -d --net host -v twsnmpfc:/datastore twsnmp/twsnmpfc
```

WindowsやMac OSのデスクトップ版Docker環境の場合は、

```sh
docker  volume create twsnmpfc 
docker  run  --rm -d --sysctl net.ipv4.ping_group_range="0 65535" -p 8080:8080 -v twsnmpfc:/datastore  twsnmp/twsnmpfc
```

のように起動します。この場合、ARP監視やデバイスレポートの動作に制限があります。
--sysctl net.ipv4.ping_group_range="0 65535"は、PINGをudpモードで実施する時だけ必要です。

# ブラウザーから動作確認

ブラウザーから

```
http://<TWSNMP FCのIP>:8080/
```

※ 8080はデフォルトのポート番号、変更した場合は合わせてください。

にアクセスすると

![](/images/books/twsnmpfc-manual/1652597163053-coEfgGH8lM.png)

のような画面が表示さます。
＜ログイン＞ボタンをクリックしてログイン画面

![](/images/books/twsnmpfc-manual/picture_pc_07513ea8f12c46bdc63dd0faed8571a4.png)

を表示して初期アカウント

```
ユーザーID:twsnmp
パスワード:twsnmp
```

でログインできればインストールは成功です。

おめでとうございます！！
