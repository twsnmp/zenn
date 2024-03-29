---
title: "PING"
---

管理対象ノードにPINGを実施する機能の説明です。

# 動画マニュアル

https://youtu.be/eVWcjkhz7WU

# PING画面を表示する方法

マップ上のノードを右クリックして「PING」メニューをクリックします。

![](/images/books/twsnmpfc-manual/2022-08-01_17-02-43.png)

または、ノード情報のダイアログの＜操作メニュー＞ボタンから「PING」をクリックします。

![](/images/books/twsnmpfc-manual/2022-08-01_17-03-04.png)


# PING画面

初期状態では、

![](/images/books/twsnmpfc-manual/2023-02-01_04-53-48.png)

のような画面です。

宛先のIPアドレス、回数、サイズ、TTLを変更できます。

実行すると

![](/images/books/twsnmpfc-manual/2023-02-01_04-57-30.png)

のように結果が表示できます。
動作は、

![](/images/books/twsnmpfc-manual/picture_pc_7f3ebce899c83f6c71cf6854ea333236.gif)

のような感じです。

# ヒストグラム

応答時間のばらつきを見るためにヒストグラムを表示できます。

![](/images/books/twsnmpfc-manual/1652558530438-feoCpd3ebq.png)

# ３Dグラフ

サイズを変化させるモードで実行した場合は、サイズ、応答時間、実行日時の関係を３Dのグラフで表示できます。

![](/images/books/twsnmpfc-manual/1652558599023-umjWVq7qdi.png)

# 回線速度予測

サイズを変化させた実行した場合に、回線速度を予測することもできます。

![](/images/books/twsnmpfc-manual/1652558671180-AjuzSEIcvL.png)

サイズと応答時間の関係を線形回帰分析して直線の傾きと切線を得ています。傾きが回線速度、切線が固定的な回線の遅延時間になります。
とは言っても回線速度は、それほど正確に測定はできません。PINGだとデータサイズが小さすぎるが問題だと思います。


# トレースルート

TTLの設定で「トレースルート」を選択するして実行すると、送信するTTLの値を１ずつ増やしながら
PINGを実行します。

![](/images/books/twsnmpfc-manual/2023-01-31_06-39-42.png)
# 位置情報

IP位置情報データベースの設定をしておけばPINGの宛先やトレースルートの経路上の
ルータの位置を世界地図に表示できます。

![](/images/books/twsnmpfc-manual/2023-01-31_06-40-00.png)
