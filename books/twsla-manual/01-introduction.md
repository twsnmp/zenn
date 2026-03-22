---
title: "はじめに・基本的な使い方"
---
# TWSLA (TWSNMP's Simple Log Analyzer)

TWSLA は、超高速の設定不要の CLI ログ アナライザーです。複雑な ELK スタックを設定せずに、大量のログからパターンを即座に grep、カウント、視覚化する必要があるシステム管理者向けに設計されています。Linux/Mac OS/Windowsで動作します。

![](/images/twsla/twsla.png)

## インストール

Linux/Mac OSはシェルスクリプトでインストールするのがオススメです。

```bash
$curl -sS https://lhx98.linkclub.jp/twise.co.jp/download/install.sh | sh
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
  relation    Relation Analysis
  search      Search logs.
  sigma       Detect threats using SIGMA rules
  tfidf       Log analysis using TF-IDF
  time        Time analysis
  twlogeye    Import notify,logs and report from twlogeye
  twsnmp      Get information and logs from TWSNMP FC
  version     Show twsla version
```

## ソースコード

ソースコードは、GitHubで公開しています。
[https://github.com/twsnmp/twsla](https://github.com/twsnmp/twsla)

