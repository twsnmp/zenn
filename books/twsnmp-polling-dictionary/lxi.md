---
title: "LXI 監視"
---
# LXI 監視

## LXI（LAN eXtensions for Instrumentation）とは
LXIは、イーサネット（LAN）をベースとした計測機器の統合・接続のためのオープンな国際標準規格です。
従来のGPIB（IEEE-488）やVXI/PXIなどの計測器専用インターフェースに代わり、広く普及しているLAN技術を活用することで、計測システムを高速かつ低コストに構築することを目的としています。

- **標準化**: LXI Consortiumによって策定・管理されています。
- **主な特徴**:
    - **Webサーバー機能**: 多くのLXI機器はWebブラウザから設定や確認が可能なWeb UIを備えています。
    - **標準通信プロトコル**: VXI-11、HiSLIP、またはポート5025などを使用したRaw Socket通信が標準化されています。
    - **タイミングと同期**: IEEE 1588 (PTP) を使用した高精度な時刻同期や、LAN経由のトリガーをサポートします（対応機のみ）。
    - **遠隔制御**: SCPI（Standard Commands for Programmable Instruments）などのコマンドセットを使用してネットワーク経由で制御可能です。

## 概要
TWSNMPのLXI監視は、LXI準拠の計測器（オシロスコープ、デジタルマルチメーター、電源など）に対して、ネットワーク経由でSCPIコマンドを送信し、その応答をJavaScriptで解析して監視状態を決定するポーリングです。

## ポーリング設定
- **種別**: `lxi`
- **パラメータ**: LXIアドレス、またはポート番号を指定します。
    - **空欄の場合**: `TCPIP0::<NodeIP>::5025::SOCKET` (デフォルトのSCPIポート) を使用します。
    - **数値（ポート番号）のみの場合**: `TCPIP0::<NodeIP>::<ポート番号>::SOCKET` を使用します。
    - **フルアドレスの例**:
        - `TCPIP::<NodeIP>::INSTR` (VXI-11プロトコル)
        - `TCPIP::<NodeIP>::5025::SOCKET` (Raw Socket)
        - `VXI11::<NodeIP>::INSTR`
- **スクリプト**: JavaScriptで記述します。最後に評価された値が `true` なら正常、`false` なら異常（指定したレベル）になります。

## JavaScript専用関数
LXI監視のスクリプト内では以下の関数が利用可能です。

### `lxiCommand(command, ...args)`
計測器へコマンドを送信します（応答を要求しない命令用）。
- **引数**:
    - `command`: コマンド文字列（例：`":DISPlay:CLEar"`）
    - `args`: 可変長引数（数値や文字列をコマンドに付与できます）
- **戻り値**: 送信成功なら `true`、失敗なら `false`

### `lxiQuery(query, [timeout])`
計測器へクエリを送信し、その応答を戻り値として取得します。
- **引数**:
  - `query`: クエリ文字列（例：`"*IDN?"`, `":MEASure:VOLTage:DC?"`）
  - `timeout`: （任意）ミリ秒単位のタイムアウト値
- **戻り値**: 応答文字列。失敗またはタイムアウト時は `undefined`
