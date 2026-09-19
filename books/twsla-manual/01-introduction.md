---
title: "はじめに・基本的な使い方"
---
# TWSLA (TWSNMP's Simple Log Analyzer)

TWSLA は、超高速の設定不要の CLI ログ アナライザーです。複雑な ELK スタックを設定せずに、大量のログからパターンを即座に grep、カウント、視覚化する必要があるシステム管理者向けに設計されています。Linux/Mac OS/Windowsで動作します。

![](/images/twsla/twsla.png)

## インストール

Linux/Mac OSはシェルスクリプトでインストールするのがオススメです。

```bash
curl -sS https://raw.githubusercontent.com/twsnmp/twsla/main/install/install.sh | sh
```

Linux/Mac OSはhomebrewでもインストールできます。

```bash
$brew install twsnmp/tap/twsla
```

Windowsは、リリースからZIPファイルをダウンロードするかscoopでインストールします。

```powershell
>scoop bucket add twsnmp https://github.com/twsnmp/scoop-bucket
>scoop install twsla
```

## 基本的な使い方

- 作業用のディレクトリを作成します。
- そのディレクトリに移動します。
- ログをimportコマンドでインポートします。
- searchコマンドで検索します。
- 結果をCSVなどに出力できます。

```bash
~$mkdir test
~$cd test
~$twsla import -s <Log file path>
~$twsla search
```

## コマンド体系

対応しているコマンドを図示すると以下のようになります。

![](https://assets.st-note.com/img/1731635423-vj6JTY1yz0eEg9l4pdIskRKh.png?width=1200)

`help`コマンドで対応しているコマンドを確認できます。

```bash
Simple Log Analyzer by TWSNMP

Usage:
  twsla [command]

Available Commands:
  ai          AI-powered log analysis
  anomaly     Anomaly log detection
  completion  Generate the autocompletion script for the specified shell
  count       Count log
  delay       Search for delays in the access log
  email       Search or count email logs
  extract     Extract data from log
  heatmap     Command to tally log counts by day of the week and time of day
  help        Help about any command
  import      Import log from source
  mcp         MCP server
  model       Manage local LLM models
  relation    Relation Analysis
  search      Search logs.
  sigma       Detect threats using SIGMA rules
  tfidf       Log analysis using TF-IDF
  time        Time analysis
  twlogeye    Import notify,logs and report from twlogeye
  twsnmp      Get information and logs from TWSNMP FC
  update      Update twsla to the latest or specified version
  version     Show twsla version
```

## v2.0.0〜v2.2.0 の主な強化ポイント

- **内蔵ローカルLLM (tensai) と `model` コマンド**: 外部Ollamaサーバー不要で、PCローカルのGPU（Metal, DirectX, Vulkan）を使って高速にAI推論・ログ分析を実行可能。
- **Sigmaルール脅威検知の強化 (`sigma`)**: 75種類の組み込みSigma/Wazuhルールパックを標準搭載。ディレクトリ指定なしで即座に脅威スキャンを実行。
- **データストア形式の拡充**: 従来のbbolt（`.db`）に加え、列指向で超高圧縮な **Apache Parquet**（`.parquet`）や高速な **Badger**（`.badger`）に対応。
- **MCPサーバー (`mcp`)**: Claude Desktopなどの生成AIツールから直接twslaを呼び出してログ分析を依頼できるModel Context Protocolサーバー機能を搭載。
- **データソース拡張**: FTP/FTPSインポート、twlogeye統合（Grafana Loki, Elasticsearch, OpenSearch）に対応。

## ソースコード

ソースコードは、GitHubで公開しています。
[https://github.com/twsnmp/twsla](https://github.com/twsnmp/twsla)

