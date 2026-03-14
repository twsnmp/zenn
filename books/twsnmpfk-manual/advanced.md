---
title: "高度な連携機能"
---

## OpenTelemetry

OpenTelemetryコレクターとして動作し、メトリック、トレース、ログを受信して可視化します。

### メトリック・トレース・ログ
- **メトリック**: リソースの推移をチャート表示。
- **トレース**: サービス間の呼び出し関係をDAGやタイムラインで可視化。
- **ログ**: 受信したスパンログ等の検索。

![](/images/twsnmpfk/ja/2025-05-25_16-47-58.png)
![](/images/twsnmpfk/ja/2025-05-25_16-51-04.png)

## MQTT

内蔵のMQTTブローカー（または外部連携）を通して、トピックの監視や受信データのSyslog変換が可能です。

![](/images/twsnmpfk/ja/2025-11-22_04-56-15.png)

## MCPサーバー

AIアシスタント（ClaudeやChatGPTなど）からTWSNMP FKのデータを読み取り、操作するためのMCP (Model Context Protocol) サーバー機能を搭載しています。

![](/images/twsnmpfk/ja/2025-07-25_04-43-13.png)

## AI分析 (Isolation Forest)

ポーリング結果の数値データをAIで分析し、通常とは異なる動きを「異常スコア（偏差値）」として算出して検知します。

![](/images/twsnmpfk/ja/2023-11-28_04-32-55.png)
![](/images/twsnmpfk/ja/2023-11-28_04-43-51.png)
