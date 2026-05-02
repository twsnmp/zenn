---
title: "TwLogEye 統合監視"
---
# TwLogEye 統合監視

## 概要
姉妹機 [TwLogEye](https://github.com/twsnmp/twlogeye)（ログ監査ツール）の解析レポートおよび通知をポーリングして、TWSNMP側で異常検知やアラート管理を行うための統合監視機能です。gRPCを使用して通信を行い、ログの正規化結果や統計情報、AIによる異常スコアを監視のフックとして利用できます。

## ポーリング設定

- **種別**: `twlogeye`
- **モード**: 監視対象のレポート種別または通知レベルを指定します。
    - レポート系: `report.syslog`, `report.trap` (または `report.snmptrap`), `report.netflow`, `report.winevent`, `report.anomaly`
    - 通知系: TwLogEyeの通知レベル（`high`, `medium`, `low`, `info`, `none`）
- **パラメータ**: TwLogEye의 gRPCサーバーのポート番号を指定します（デフォルト: `8081`）。
- **フィルター**: 通知系（Notify）モードの場合、ログメッセージを絞り込むための正規表現を指定できます。
- **スクリプト**: 取得した指標（Metrics）を判定するためのJavaScript（Ottoエンジン）。

## 取得指標 (Metrics)

各モードで取得され、判定スクリプト内で利用可能な変数の一覧です。

### 全モード共通
- `interval`: ポーリング間隔（秒）

### Syslogレポート (`report.syslog`)
- `errors`: エラー件数
- `warns`: 警告件数
- `normal`: 正常件数
- `patterns`: 出現したパターンの総数
- `errPatterns`: エラーパターンの総数

### SNMP Trapレポート (`report.trap` / `report.snmptrap`)
- `count`: トラップの総件数
- `types`: トラップの種類の数

### NetFlowレポート (`report.netflow`)
- `bytes`: 送信バイト数
- `flows`: フロー数
- `fumbles`: 不正なフロー数（Fumbles）
- `IPs`: 登場したIPアドレス数
- `MACs`: 登場したMACアドレス数
- `protocols`: 登場したプロトコル数
- `packets`: 送信パケット数

### Windows Eventレポート (`report.winevent`)
- `errors`: エラーイベント数
- `warns`: 警告イベント数
- `normal`: 情報レベル等のイベント数
- `types`: イベントIDの種類の数
- `errTypes`: エラー/警告イベントIDの種類の数

### 異常検知レポート (`report.anomaly`)
TwLogEyeで定義された各異常検知タイプのスコアが変数名として提供されます。
- `<Type>_Score`: 各タイプの異常スコア（例: `syslog_Score`, `netflow_Score` など）

### 通知 (`high`, `medium` 等)
- `count`: 前回の実行以降に発生した指定レベルの通知件数
- `lastLog`: 最後に取得した通知内容（文字列）
