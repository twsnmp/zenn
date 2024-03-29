---
title: "とりあえずマップを作る"
---


TWSNMP FCを起動できたら、とりあえず管理マップを作って使ってみるのがよいと思います。
ネットワーク管理の理論、システム設計とか難しく考えてもそれほど厳密に監視できているケースはないと思っています。
これから案内する方法で管理マップを作れば、すくなくとも使っているネットワークをどのような機器が利用しているか見ることができます。
では、説明をはじめます。

# 動画マニュアル

https://youtu.be/BNpiZLwiZRo

# マップに名前をつける

メニューの「システム設定」-「マップ」をクリックをすれば、マップ設定の画面が表示されます。
とりえず、「マップ名」にマップの名前を入力して<保存>ボタンをクリックします。
「名前を何にすればよいか？」悩むようなら"test"とか自分の名前とかにしておけばよいです。

![](/images/books/twsnmpfc-manual/2023-01-29_05-16-58.png)

# 自動発見で監視対象ノードを登録する

マップ上のノードを配置を開始したい場所を右クリックしてメニューから

![](/images/books/twsnmpfc-manual/picture_pc_8c466d1d0f1e48aa715a8aba671812c4.png)

「自動発見」をクリックします。自動発見の設定が表示されます。

![](/images/books/twsnmpfc-manual/2022-07-02_05-38-40.png)

検索する範囲のIPアドレスを設定して<開始>ボタンをクリックします。

ちゃんと発見できるか心配は人は、アクティブモードにしてタイムアウトとリトライ回数を大きくすればよいです。
SNMPのCommunityが何かわかっていてpublicは違うと思ったらマップ設定で変更すればよいです。
何のことかわからない場合は、そのままでよいです。しばらくすれば自動発見の進行が表示されます。

![](/images/books/twsnmpfc-manual/picture_pc_9d2b8288ff614423c1ab50c075bb0c4d.png)

マップ画面に切り替えれば、マップ上にノードが現れます。イベントログに発見や終了などの自動発見の状況が表示されます。
何も発見しないのであれば、アドレスの範囲が間違っていたのだと思います。

:::message alert
※厳しいネットワーク管理者が管理しているネットワークで、自動発見をアクティブモードで実施するとノードスキャンを検知して怒られるかもしれないので注意してください。古いTWSNMPや復刻版よりもFC版はより詳しくノードを調べるので怒られる可能性が高くなります。
:::

# ノードの配置を変える

自動発見でノードが登録されたらノードをドラックして好きな位置に移動します。どこに移動するかは、お好きなように決めてください。インターネットに接続するルーターやサーバーを上の方にHUBを真ん中に配置して周りにパソコンを配置するとスッキリすると思います。

# アイコンを変える

ノードを右クリックしてメニューから「編集」を選択します。
ノード設定の画面でアイコンを変更できます。

![](/images/books/twsnmpfc-manual/2023-01-29_05-21-51.png)

# ラインを接続する

ノードの位置がだいたい決まったらノードの間にラインを描きます。１つ目のノードをクリックして選択した後、シフトキーを押しながら２つ目のノードをクリックするとライン設定が表示されます。ラインの色を決めるポーリングを選択して＜保存> をクリックすれば、ラインが接続できます。

![](/images/books/twsnmpfc-manual/2023-01-29_05-19-08.png)

SNMPに対応しているノードには、LANポートの状態を示すポーリングが登録されていますが、それ以外は、PINGしか登録されていません。
LANポートの状態を示すポーリングを使えばラインの色で実際の接続状態を表現することができますが、わからなければ両方PINGのポーリングを選択して<保存>ボタンをクリックすればよいです。

![](/images/books/twsnmpfc-manual/picture_pc_02d77921a752f5a2e45bc4981ad271e3.gif)

復刻版にはないラインに情報を表示する設定や太さも変更できますが、詳しい話は別の機会に書きます。

# マップの背景を変える

「システム設定」ー「マップ」の画面で＜背景設定＞ボタンをクリックします。


![](/images/books/twsnmpfc-manual/2023-01-29_05-24-47.png)

背景の画像と色を変更できます。
