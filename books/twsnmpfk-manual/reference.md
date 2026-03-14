---
title: "リファレンス"
---

## データストア内のファイル

データフォルダ内の以下のファイルをカスタマイズまたはバックアップに利用できます。

- `twsnmpfk.db`: データベースファイル。
- `extmibs/*`: 追加MIBファイル。
- `icons/*`: オリジナルアイコン素材。
- `.twsnmpfk.ini`: 起動パラメータを記述する設定ファイル。

## 起動パラメータ

コマンドラインから指定可能な主なオプションです。

|パラメータ|説明|デフォルト|
|---|---|---|
|`-datastore`|データフォルダのパス|カレント|
|`-syslogPort`|Syslog受信ポート|514|
|`-trapPort`|SNMP TRAP受信ポート|162|
|`-otelHTTPPort`|OpenTelemetry HTTP受信ポート|4318|
|`-mqttTCPPort`|MQTTサーバーポート|1883|

## 設定ファイル例 (.twsnmpfk.ini)

```ini
# 言語設定
lang=ja

[logger]
syslogPort=8514
trapPort=8162
netflowPort=2056

[OTel]
otelHTTPPort=4318
```

詳細なパラメータはヘルプコマンド（`--help`）で確認してください。
