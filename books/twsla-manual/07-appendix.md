---
title: "付録 (対応ログ・フィルタ設定等)"
---

# ユーティリティコマンド

- **`version` コマンド**: TWSLAの現在のバージョンを表示します。
- **`update` コマンド**: GitHub Releasesからtwslaを最新版（または指定バージョン）に自動更新します（`-c` でチェックのみ、`-y` で確認省略）。
- **`completion` コマンド**: `bash`, `fish`, `powershell`, `zsh` に対応したコマンド補完用のスクリプトを生成します。

```bash
# シェル補完スクリプトの生成（bash例）
$ twsla completion bash > /etc/bash_completion.d/twsla

# 最新版へのアップデート
$ twsla update -y
```

---

# 対応しているログとデータストア形式

TWSLAは様々な形式のログに対応しています（テキストファイル、圧縮されたZIPやtar.gzファイル等も直接読み込み可能）。

### 対応ログ
- １行毎にタイムスタンプのあるテキストファイル (.gz / .tar.gz / .zip)
- 複数行にまたがるスタックトレースやログ（`--mlStart`, `--mlSep`, `--mlLines`, `--mlInspect`）
- Windows イベントログ (.evtx)（JSON形式の表示も可）
- 電子メール (.eml) および IMAP/POP3/IMAPS/POP3S サーバー上のメール
- Grafana Loki (`loki://`, `lokis://`)
- Elasticsearch / OpenSearch (`es://`, `os://`)
- TWSNMP FC / TwLogEye の内部ログやアラート

### サポートするデータストアエンジン (`-d`)
- **Apache Parquet (`.parquet`)**: 列指向圧縮による超高速集計・省ストレージ（DuckDB/Python等とも直接連携可能）
- **Badger (`.badger`)**: 高速なLSMツリーベースのKVS
- **Bbolt (`.db`)**: 安定した組み込みB+ Treeデータベース（デフォルト）

---

# 各種フィルター指定と集計・抽出の指定

## 1. フィルターの種類

TWSLAの特徴として、「シンプルフィルター（`-f`）」と「正規表現フィルター（`-r`）」があります。両方を指定した場合はAND条件になります。
- シンプルフィルター例: `Message*` (正規表現の `Message.*` に相当)
- コマンドライン引数でのフィルター指定: フィルター文字列の先頭を `^` にすると除外（反転）フィルターとして動作します。

また、頻繁に利用されるパターンとして、`#IP`, `#MAC`, `#EMAIL`, `#URL`, `#CREDITCARD`, `#MYNUMBER`, `#UUID` などの便利なキーワードによるフィルタリングにも対応しています。

## 2. 直感的な時間範囲指定

`-t` オプションで時間範囲を指定する際、直感的な略記法に対応しています。

```bash
# 2024年1月1日から1日間
-t 2024/1/1,1d

# 過去1時間
-t -1h
```

## 3. データ抽出パターンの簡易な指定

ログからのデータ抽出は、`-e`オプションと`-p`オプションで行います。

**代表的な抽出パターン:**
- `ip`, `ipv6`, `mac`, `email`, `url`, `number`, `uuid`
- `loc`, `country`, `host`, `domain` (ホストや位置情報等の逆引き - IPから)

より高度な抽出には、GROKパターンの組み込みサポート（`-g`, `-x`指定）や、JSONログ内からのJSONPATHでのデータ抽出をサポートします。

---

# 設定ファイルと環境変数

設定値は「ホームディレクトリの `.twsla.yaml`」や環境変数で制御可能です。

**主な環境変数:**
- `TWSLA_DATASTORE`: データストア（`.parquet`, `.badger`, `.db`）のパス
- `TWSLA_GEOIP`: GeoIPデータベースファイルパス（位置情報集計に必須）
- `TWSLA_GROK`: 独自のGROK定義ファイルのパス
- `TWSLA_SIXEL`: Sixelを用いたターミナル内のインライングラフ表示をオンにする (`true` にする)
- `OPENAI_API_KEY` / `ANTHROPIC_API_KEY` / `GOOGLE_API_KEY`: 各社LLMと連携するためのAPIキー

---

> この説明に使ったサンプルのログは提供元のリポジトリまたは [loghub](https://github.com/logpai/loghub) をご参照ください。

