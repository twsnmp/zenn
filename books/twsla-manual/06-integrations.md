---
title: "連携・外部統合 (twsnmp・email・twlogeye・mcp)"
---

# twsnmpコマンド

![](/images/twsla/twsnmp.png)

TWSNMP FC（またはFK）と連携して情報やログを取得するためのコマンドです（v1.4.0〜）。

```bash
twsla twsnmp [target] [flags]
```

`target` には `node`, `polling`, `eventlog`, `syslog`, `trap`, `netflow`, `ipfix`, `sflow` 等が指定できます。
`--twsnmp` オプションでTWSNMP FCのURL（例: `http://user:password@192.168.1.250:8080`) を指定します。

出力はTAB区切りのテキストとなっており、`--jsonOut` を追加すればJSON形式で出力可能です。

---

# emailコマンド

![](/images/twsla/email.png)

IMAP/POP3などからインポートしたメールのログを検索したり、送信元等の情報を集計するためのコマンドです。メールヘッダーから計算した遅延時間とリレー回数も確認・ソート（`d`キー・`r`キー）可能です。

```bash
twsla email [search|count] [flags]
```

- `search` サブコマンド: メールを検索し、`Enter` で詳細を表示。
- `count` サブコマンド: `--emailCountBy` オプションに `time`（デフォルト）、`from`, `to`, `matrix`, `subject`, `ip`, `domain`, `spf`, `spf.list` などを指定することで、メール情報の種別ごとに集計を行います。
`--checkSPF` を指定すると、集計時にSPFの検証を自動で行います。

---

# twlogeye と外部ログ基盤との連携

![](/images/twsla/twlogeye.png)

ログサーバー「TwLogEye」や外部ログ基盤から直接ログやアラートを取り込むことができます。

### 1. TwLogEye連携 (`import twlogeye://...`)
gRPCを利用して、脅威検知アラートやログ、レポートをインポートします（以前の `twlogeye` コマンドと同等）。

```bash
# 通知アラートの取り込み
twsla import -s twlogeye://192.168.1.1:8081

# 特定ログの取り込み
twsla import -s twlogeye://192.168.1.1:8081/logs/syslog

# 異常検知レポートの取り込み
twsla import -s twlogeye://192.168.1.1:8081/report/anomaly/monitor
```

### 2. Grafana Loki / Elasticsearch / OpenSearch 連携
URLスキーマを指定することで、クラウドやサーバー上のログストアから直接インポートできます：

```bash
# Grafana Loki から LogQL を指定してインポート
twsla import -s loki://192.168.1.1:3100 --lokiQuery '{job="syslog"}'

# Elasticsearch / OpenSearch からインポート
twsla import -s es://192.168.1.1:9200/my-logs-*
```

---

# mcp コマンド (Model Context Protocol)

![](/images/twsla/mcp.png)

Claude Desktop、Cline、Cursor、Antigravityなどの**AIエージェントとTWSLAを連携させるMCPサーバー**を立ち上げるコマンドです。

```bash
twsla mcp [flags]
```

### 主なオプション
- `--transport`: 通信方式（`stdio` (標準入出力・デフォルト), `sse`, `stream`）
- `--endpoint`: ネットワーク経由時のバインドアドレス（デフォルト `127.0.0.1:8085`）
- `--clients`: 接続を許可するクライアントIPのホワイトリスト（カンマ区切り）
- `--geoip`: 位置情報解決用のGeoIPデータベースパス

### AIエージェントに公開されるツール (Tools)
AIは以下のツールを自律的に呼び出し、ログ分析・脅威調査を実施します：

| ツール名 | 説明 |
|---|---|
| `search_log` | フィルタや時間範囲を指定してログを検索 |
| `count_log` | 時間、IP、メール、ドメイン、単語、正規化パターン等でグループ化集計 |
| `extract_data_from_log` | IP、MAC、数値、正規表現パターンに合致するデータを抽出 |
| `import_log` | 指定したファイルやディレクトリのログをデータベースに取り込み |
| `get_log_summary` | エラー/警告数や頻出エラーパターンを含むログ全体のサマリーを取得 |
| `detect_threats_sigma` | 内蔵またはカスタムSigmaルールを用いて脅威を自動検知 |
| `detect_anomalies` | Isolation ForestやAutoEncoder等の機械学習を用いて異常ログを検知 |
| `analyze_relations` | ログ内の要素間（IP、MAC、URL等）の共起関係を有向グラフ分析 |
| `analyze_tfidf` | TF-IDFを用いて出現頻度の極めて低いレアな異常ログを抽出 |

### 提供されるリソースとプロンプト
- **リソース**: `twsla://db/status`（DB種別、総件数、期間情報）、`twsla://sigma/rules`（内蔵Sigma設定定義）
- **プロンプト**: `incident_investigation`（インシデント調査手順）、`security_threat_hunt`（脅威ハンティング）、`anomaly_audit`（外れ値監査）

### Claude Desktopでの設定例 (`claude_desktop_config.json`)
```json
{
  "mcpServers": {
    "twsla": {
      "command": "twsla",
      "args": ["mcp", "-d", "/path/to/twsla.parquet"]
    }
  }
}
```
設定後、Claude DesktopなどのAIアシスタントに「過去24時間のエラーログの傾向を分析して」「Sigmaルールで攻撃を調査して」と指示するだけで、AIが自動的にTWSLAの各機能を駆使して分析レポートを作成してくれます。

