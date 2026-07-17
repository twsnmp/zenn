---
title: "個人開発や学習に最適！TWSNMP FC/FK を簡易コレクターにして OpenTelemetry (OTLP) をサクッと理解する"
emoji: "🔭"
type: "tech"
topics: ["opentelemetry", "twsnmp", "go", "observability"]
published: true
---

# はじめに

近年、システムの運用監視や分析におけるデファクトスタンダードとして確固たる地位を築いた「**OpenTelemetry (OTel)**」。
「そろそろ自分も学んでみたい」「開発中のアプリケーションが正しくテレメトリーデータ（メトリクス、ログ、トレース）をエクスポートできているか検証したい」と思う方も多いのではないでしょうか。

しかし、いざ手を動かそうとすると、以下のような環境構築のハードルに直面しがちです。

- 本格的な **OpenTelemetry Collector** を立ち上げるための複雑な YAML 設定に苦戦する。
- 可視化バックエンドとして Prometheus や Jaeger、Loki などを Docker Compose で何個も起動し、リソースを圧迫する。
- 商用の可観測性（Observability）SaaS のアカウントを登録して接続設定をするのが面倒、あるいはテストデータをインターネット経由で送りたくない。

もっと手軽に、**ローカル環境だけで完結し、かつ追加のミドルウェア構築なしでテレメトリーを受信・可視化できる方法**はないでしょうか？

実は、日本で25年以上の歴史を持つネットワーク管理ソフトの現代版「**TWSNMP FC / FK**」には、**簡易的な OpenTelemetry コレクター（OTLP レシーバー）機能が標準で内蔵されています**。

マップ設定のチェックボックスを1つ ON にするだけで、OTLP によるデータ受信を開始し、内蔵のUIでログ検索、メトリクスのグラフ化、そしてトレースのガントチャート表示までをローカル完結で行えます。

この記事では、TWSNMP FC/FK を簡易コレクターとして活用し、**Go言語のテストプログラム**からテレメトリーデータを送信してモニタリングする具体的な手順を紹介します。

---

# TWSNMP FC/FK の OpenTelemetry 機能とは？

**TWSNMP FC**（Web/Docker版）および **TWSNMP FK**（デスクトップアプリ版）は、PING、SNMP、Syslog、Netflow などを用いてネットワーク全体を管理するオープンソースのツールです。

ネットワーク機器の監視だけでなく、現代のクラウドネイティブなコンテナやアプリケーションの状態も一元的に監視できるようにするため、TWSNMP には OpenTelemetry (OTel) の受信機能が実装されています。

TWSNMP でこの機能を有効化すると、内部で OTLP レシーバーデーモンが起動し、以下のデフォルトポートでテレメトリーデータの待ち受けを開始します。

* **gRPC ポート**: `4717`
* **HTTP ポート**: `4718` (JSON / Protobuf)

送信側のアプリケーションから、エンドポイントとして `http://localhost:4718` (HTTP) または `localhost:4717` (gRPC) を指定するだけで、特別なプロキシやコレクターを中継することなく、TWSNMP が直接データを受け取ってくれます。

---

# TWSNMP で OpenTelemetry を有効にする手順

設定は非常に簡単です。

1. TWSNMP の管理画面から **[マップ設定]** を開きます。
2. **[OpenTelemetry]** の項目（チェックボックス）を ON にします。
3. 必要に応じて、受信を許可する IP アドレス（送信元制限）や、データの保存時間を設定します。
4. 設定を保存します。

これだけで、TWSNMP は簡易コレクターとして動作を開始します。

*(※以下は TWSNMP FK のマップ設定画面です。下部にある「OpenTelemetry」にチェックを入れて保存します)*

![](/images/twsnmp-opentelemetry-guide/map_setting.png)

---

# 実践：Go言語のテストプログラムから送信する

まずは、OpenTelemetry の仕様（SDKの扱い方）を学ぶために、簡単な Go 言語のアプリケーションを作成して、TWSNMP にテレメトリーを送信してみましょう。

ここでは、OpenTelemetry 公式の Getting Started にあるサイコロを振るプログラム（`rolldice`）をベースに、出力先をコンソール（stdout）から TWSNMP が待つ OTLP HTTP エンドポイントへ変更する例を紹介します。

### 1. 送信プログラムの実装

Go アプリケーション側のプロバイダー設定を、以下のように OTLP HTTP エクスポーターに向けて定義します。

`WithEndpointURL` を使用して、TWSNMP が待ち受けるHTTPエンドポイント（ポート `4718`）のシグナルパス（`traces`、`metrics`、`logs`）をそれぞれ完全なURL形式で指定します。この書き方の場合、`http://` スキーマから自動的に TLS なしの HTTP 通信と判断されるため、明示的な `WithInsecure()` の指定が不要になり、よりスッキリ記述できます。

```go
package main

import (
	"context"
	"time"

	"go.opentelemetry.io/otel"
	"go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploghttp"
	"go.opentelemetry.io/otel/exporters/otlp/otlpmetric/otlpmetrichttp"
	"go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracehttp"
	"go.opentelemetry.io/otel/log/global"
	sdklog "go.opentelemetry.io/otel/sdk/log"
	sdkmetric "go.opentelemetry.io/otel/sdk/metric"
	sdktrace "go.opentelemetry.io/otel/sdk/trace"
)

// トレースプロバイダーの初期化
func initTracer() (*sdktrace.TracerProvider, error) {
	// 送信先を TWSNMP の OTLP HTTP ポート (4718) の traces パスに指定
	exporter, err := otlptracehttp.New(context.Background(),
		otlptracehttp.WithEndpointURL("http://localhost:4718/v1/traces"),
	)
	if err != nil {
		return nil, err
	}

	tp := sdktrace.NewTracerProvider(
		sdktrace.WithBatcher(exporter, sdktrace.WithBatchTimeout(1*time.Second)),
	)
	otel.SetTracerProvider(tp)
	return tp, nil
}

// メトリクスプロバイダーの初期化
func initMeter() (*sdkmetric.MeterProvider, error) {
	// 送信先を TWSNMP の OTLP HTTP ポート (4718) の metrics パスに指定
	exporter, err := otlpmetrichttp.New(context.Background(),
		otlpmetrichttp.WithEndpointURL("http://localhost:4718/v1/metrics"),
	)
	if err != nil {
		return nil, err
	}

	mp := sdkmetric.NewMeterProvider(
		sdkmetric.WithReader(sdkmetric.NewPeriodicReader(exporter, sdkmetric.WithInterval(5*time.Second))),
	)
	otel.SetMeterProvider(mp)
	return mp, nil
}

// ログプロバイダーの初期化
func initLogger() (*sdklog.LoggerProvider, error) {
	// 送信先を TWSNMP の OTLP HTTP ポート (4718) の logs パスに指定
	exporter, err := otlploghttp.New(context.Background(),
		otlploghttp.WithEndpointURL("http://localhost:4718/v1/logs"),
	)
	if err != nil {
		return nil, err
	}

	lp := sdklog.NewLoggerProvider(
		sdklog.WithProcessor(sdklog.NewBatchProcessor(exporter)),
	)
	global.SetLoggerProvider(lp)
	return lp, nil
}
```

### 2. TWSNMP でのデータ確認

プログラムを実行し、HTTP リクエストを送るなどしてテレメトリーデータを発生させます。

TWSNMP の Web UI（またはデスクトップのログ画面）から **[ログ] -> [OpenTelemetry]**（またはデスクトップ版の OTel ログ画面）を開くと、送信されたデータがリアルタイムに記録されているのを確認できます。

![](/images/twsnmp-opentelemetry-guide/metric_receive.png)

- **トレース表示**:
  特定のリクエストをクリックすると、どの関数（スパン）で処理がどれくらいかかったかが、分かりやすいガントチャート形式で可視化されます。データベースへのクエリ時間や外部APIの遅延テストに非常に便利です。

  ![](/images/twsnmp-opentelemetry-guide/trace_receive.png)

  *(※特定のトレースをクリックすると、さらに詳細なガントチャート（スパンごとの処理時間）が表示されます)*
  ![](/images/twsnmp-opentelemetry-guide/trace_report.png)
- **メトリクスグラフ**:
  送信されたカスタムメトリクス（リクエスト回数、処理時間のヒストグラムなど）が自動的にグラフ化され、TWSNMP 上で時間経過に伴う変化を観察できます。

  ![](/images/twsnmp-opentelemetry-guide/metric_report.png)
- **構造化ログ**:
  送信元のリソース属性や重大度 (Severity) でフィルタリングしながらログを確認できます。

  ![](/images/twsnmp-opentelemetry-guide/log_receive.png)

---

# この環境で OpenTelemetry を学ぶメリット

本物のシステム運用で OpenTelemetry を利用する場合は、複数のコレクターや可視化用の SaaS、大量のストレージサーバーを組み合わせた複雑な構成が必要です。しかし、**学習・検証の段階**においては、TWSNMP FC/FK を利用したローカル構成には以下のような際立ったメリットがあります。

1. **ミドルウェアの設定が不要で「送信側」のコード記述に集中できる**
   Collector の設定ファイル（`config.yaml`）の書き方に悩まされることなく、アプリ側の SDK 設定や計測（Instrumentation）のコードをどう書けばいいのかという学習に集中できます。
2. **完全ローカル完結で安心・安全**
   インターネットへの通信を行わず、全て自分の PC 内でクローズドに検証できるため、API キーなどの認証情報や検証用の機密データが外部に流出する心配がありません。
3. **データの中身（構造）がよく見える**
   TWSNMP は受信した OTLP の生データに近い形（JSON）を UI 上で確認しやすく、メトリクスやスパンがどのようなデータ構造で送られているのか、仕様の理解が深まります。

---

# まとめ

OpenTelemetry のコンセプトである「ベンダーに依存しないテレメトリーデータの標準化」は非常に魅力的ですが、そのエコシステムの広さゆえに、初心者の入門やテスト環境の構築には少しハードルがありました。

ネットワーク管理でお馴染みの **TWSNMP FC/FK** をローカルの簡易コレクターとして活用することで、そのハードルを大きく下げ、手軽にオブザーバビリティの世界を体験することができます。

「まずは自分のコードからトレースを送ってみたい」という方は、ぜひ TWSNMP を使った手軽なローカル OpenTelemetry テスト環境を試してみてください！

### 関連リンク

- [TWSNMP FC GitHub リポジトリ](https://github.com/twsnmp/twsnmpfc)
- [TWSNMP FK GitHub リポジトリ](https://github.com/twsnmp/twsnmpfk)
- 元記事：[OpenTelemetryのプロトコルで通信するGo言語のテストプログラムの紹介](https://qiita.com/twsnmp/items/629e0da4f7b2a2b0de1c)
