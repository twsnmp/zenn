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
- `count` サブコマンド: `--emailCountBy` オプションに `from`, `to`, `matrix`, `subject`, `ip`, `domain`, `spf` などを指定することで、メール情報の種別ごとに集計を行います。
`--checkSPF` を指定すると、集計時にSPFのチェックを自動で行います。

---

# twlogeyeコマンド

![](/images/twsla/twlogeye.png)

ログサーバー「TwLogEye」からgRPCを利用して、脅威検知アラートやログ、レポートをインポートするコマンドです。

```bash
twsla twlogeye <target> [flags]
```

`target` には `notify`、`logs`、`report` が指定でき、TwLogEyeのAPIポートや証明書などをフラグで指定します。

---

# mcp コマンド

![](/images/twsla/mcp.png)

AIエージェントなどをTWSLAと統合させるための**MCP (Model Context Protocol) サーバー**を立ち上げるコマンドです。

```bash
twsla mcp [flags]
```

AIエージェントに対して、TWSLAの各種コマンド（検索、カウント、データ抽出、サマリー取得など）をツールとして公開します。エージェント側のシステムプロンプトにTWSLAの機能情報を定義しておくことで、エージェントが自律的にログの検索や統計分析を行えるようになります。

- `--transport`: 通信方式（`stdio`, `sse`, `stream`）
- `--endpoint`: サーバーのエンドポイント（デフォルト `127.0.0.1:8085`）
- `--clients`: 接続を許可するMCPクライアントのIPリスト（カンマ区切り）
