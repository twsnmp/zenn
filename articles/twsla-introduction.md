---
title: "はじめてのTWSLA - 超高速・設定不要のCLIログアナライザー"
emoji: "🚀"
type: "tech"
topics: ["twsla", "log", "go", "cli", "twsnmp"]
published: true
---

# TWSLAとは

TWSLA (TWSNMP's Simple Log Analyzer) は、超高速の設定不要の CLI ログ アナライザーです。複雑な ELK スタックなどを設定せずに、大量のログからパターンを即座に grep、カウント、視覚化する必要があるシステム管理者向けに設計されています。Linux、Mac OS、Windowsで動作します。

![](/images/twsla/twsla.png)

## インストール
Linux/Mac OSはシェルスクリプトでインストールするのがオススメです。

```bash
curl -sS https://lhx98.linkclub.jp/twise.co.jp/download/install.sh | sh
```

あるいはHomebrewでもインストールできます。

```bash
brew install twsnmp/tap/twsla
```

Windowsは、scoopでインストールできます。

```powershell
scoop bucket add twsnmp https://github.com/twsnmp/scoop-bucket
scoop install twsla
```

## 基本的な使い方

1. 作業用のディレクトリを作成し移動します。
2. ログを `import` コマンドでインポートします。
3. `search` コマンドや `count` コマンドで検索・分析します。

```bash
mkdir test
cd test
twsla import -s <Log file path>
twsla search
```

## TWSLAの魅力

TWSLAは時系列に検索可能なデータベース（bbolt）にログを保存し、非常に高速に検索・集計を行うことができます。

- **`search` コマンド**: シンプルフィルターや正規表現でログを検索し、カラー表示も可能です。
- **`count` コマンド**: 曜日や時間単位のヒートマップ作成や、ログから特定データを抽出して集計できます。
- **`anomaly` / `ai` コマンド**: AIや機械学習（TF-IDFなど）を用いた異常検知やログ分析が可能です。

## 完全なマニュアル

すべての機能と詳細なコマンドの使い方については、
**TWSLA 完全マニュアル（Zenn Book）** 
[こちら](https://zenn.dev/twsnmp/books/twsnmpfk-manual)
としてまとめていますのでぜひご覧ください！


## ソースコード

ソースコードは、GitHubで公開しています。
[https://github.com/twsnmp/twsla](https://github.com/twsnmp/twsla)

