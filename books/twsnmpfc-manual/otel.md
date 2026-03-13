---
title: "OpenTelemetry (OTel)"
---

OpenTelemetry (OTel) プロトコルを使用して、メトリクス、トレース、ログを収集し、可視化する機能についての説明です。

# OTel画面の表示方法
メニューの「ログ」ー「OpenTelemetry」をクリックすると表示できます。

# メトリクス表示
OTelで収集したシステムのパフォーマンスメトリクスをグラフ表示します。

![](/images/books/twsnmpfc-manual/otel_metrics.png)

# トレース表示
分散トレーシングの情報を表示し、リクエストがシステム内をどのように遷移したかを可視化します。

![](/images/books/twsnmpfc-manual/otel_trace.png)

# DAG (分散グラフ) 表示
トレース情報を元に、サービス間の依存関係をDAG（有向非巡回グラフ）として表示します。システムの全体構造とボトルネックの特定に役立ちます。

![](/images/books/twsnmpfc-manual/otel_dag.png)

# ログ表示
OTel経由で送信されたアプリケーションログを表示します。

# 設定上の注意
TWSNMP FCをOTelコレクターとして動作させるためには、送信側のアプリケーションでTWSNMP FCのアドレスをエクスポート先（Exporter）として設定する必要があります。
詳細なポート番号やエンドポイントの設定は、システム構成に合わせて調整してください。
