---
title: "gNMI"
---

gRPC Network Management Interface (gNMI) プロトコルを使用して、ネットワーク機器から詳細な情報を取得する機能についての説明です。

# gNMI画面の表示方法
ノードを右クリックし、「gNMIツール」を選択します。

![](/images/books/twsnmpfc-manual/gnmi_menu.png =200x)

# gNMI設定とデータ取得
gNMIに対応した機器（Cisco, Arista, Juniperなど）に対して、Pathを指定して情報を取得します。

![](/images/books/twsnmpfc-manual/gnmi_main.png)

#### ① Path（パス）
取得したい情報のパスを指定します（例: `/components/component/state`）。

#### ② モード
取得方法（Get, Subscribeなど）を選択します。

#### ③ 取得結果
機器から返されたデータがJSON形式などで表示されます。

# gNMIポーリング
ノードのポーリング設定でgNMIを種別として選択することで、定期的に特定のパスの情報を監視し、状態の変化や閾値による判定を行うことができます。
これにより、従来のSNMPでは取得が困難だった詳細なステータスも監視可能になります。
