---
title: "自動発見"
---

TWSNMP FCにはIPアドレスの範囲を指定して自動的に監視対象のノード（パソコン、ネットワーク機器、スマフォなど）を発見する機能があります。この自動発見について説明します。


# 自動発見画面の表示方法

自動発見画面はメニューの「自動発見」から表示することができます。

![](/images/books/twlogaian-manual/picture_pc_47165b847eb519c7970e0896e6f3fb24.png)

この場合、発見したノードはマップ上の左上から配置されます。マップ上で配置したい最初の位置を右クリックしてコンテキストメニューから自動発見画面を表示することもできます。

![](/images/books/twlogaian-manual/picture_pc_979de9f732da97c011b260f2c6ddf81f.png)

# 自動発見画面

![](/images/books/twlogaian-manual/2022-07-10_17-15-18.png)

アクティブモードをオンにして基本的なポーリングをオフにした場合は、

![](/images/books/twlogaian-manual/2022-07-10_17-16-42.png)

のような感じです。

-  アクティブモード
オンにすると自動発見するときにTWSNMPから指定の範囲のIPアドレスにpingを実施します。
ネットワークのスキャンになるので注意してください。
オフにするとARPテーブルの監視で検知したIPアドレスから検索します。この場合は、
起動後にしばらく時間をおいてから実施してください。


- 開始IP
自動発見で検索する最初のIPアドレスを指定します。

- 終了IP
自動発見で検索する最後のIPアドレスを指定します。

- タイムアウト
検索する時に実施するPINGのタイムアウト値を指定します。

- リトライ回数
検索する時に実施するPINGのリトライ回数を指定します。

- 基本的なポーリングを自動追加
オンにすると自動発見の処理で判断して実施可能なポーリングを自動的に追加します。
追加するポーリングの項目は少し多すぎるので見直したいと思っています。
もしかするとPINGだけでよいかと思っています。

- 自動追加するポーリング
「基本的なポーリングを自動追加」の設定をオフにすれば、自動追加するポーリングを自分で選択できるようになります。自動追加したいポーリングにチェックをいれます。

# 自動発見の状況画面
自動発見の設定画面で＜開始＞をクリックすれば、自動発見の状況を示す画面に切り替わります。

![](/images/books/twlogaian-manual/picture_pc_6431e43bd1ff74f152d33af09749e4c5.png)

自動発見を実行中に、自動発見画面を表示すればこのの画面になります。発見の実施進行状況と発見したノードの数が表示されます。
途中で停止したい場合は＜停止＞ボタンをクリックしてください。
自動発見が完了すれば、イベントログに記録され、この画面は表示されなくなります。

# ノードの配置について
発見したノードは、指定した開始位置から横方向に配置していきます。１０ノードで折り返して次の行に配置していきます。

![](/images/books/twlogaian-manual/picture_pc_6b16021634b618bf987cccb7cad26e06.png)

# 自動発見について思っていること
オリジナルのTWSNMPでは、SNMPで取得したノードの種別からアイコンを自動で決めるようにしていました。最近は、SNMPに対応していないノードのほうが多いので、復刻版とTWSNMP FCでは対応をやめておきました。
自動発見したノードを配置する方法も少し悩んでいます。魔法のように自動で実際のネットワークを表現できる配置になればよいのですが今のところうまくやる方法のアイデアがありません。
ポーリングの自動設定も今の方法でよいのか悩んでいます。


