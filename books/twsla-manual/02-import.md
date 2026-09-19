---
title: "importコマンド"
---
# importコマンド

![](/images/twsla/import.png)

ログをインポートするためのコマンドです。時系列に検索可能なデータベースに保存します。コマンドの引数は、

```bash
$ twsla help import
Import log from source
source is file | dir | scp | ssh | twsnmp | imap | pop3

Usage:
  twsla import [flags]
```

- `-s` または `--source` で読み込むログの場所を指定します。
最新のバージョンでは `-s` オプションなしでファイルやディレクトリ名を引数で指定できます。ファイルだけを指定すれば、そのファイルのみ読み込みます。

実行例：
```bash
$ twsla import ~/Downloads/SSH.tar.gz
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│/ Loading path=/Users/ymi/Downloads/SSH.tar.gz:SSH.log line=655,147 byte=72 MB           │
│  Total file=1 line=655,147 byte=72 MB time=1.709061625s                                 │
│▆▆▆▆▆▆▆▆▆▆▆▆▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇█████████████████████████ 72 MB/Sec│
└─────────────────────────────────────────────────────────────────────────────────────────┘
```
読み込んだログの件数、サイズ、かかった時間がスパークライン付きで表示されます。

ディレクトリを指定するとディレクトリ内のファイルを一括で読み込みます。`-p` (または `--filePat`) でファイル名のパターン（シンプルフィルター構文）を指定すれば、読み込む対象を絞り込むことができます。

```bash
$ twsla import -s ~/Downloads -p "Linux*"
```

![](https://assets.st-note.com/img/1758319263-BqyMKkbUO0PT91w75IvZucgi.png?width=1200)

## 様々なデータソース

SCP、SSHやTWSNMPのログを読み込むためには、URLを指定します。
例: `scp://root@192.168.1.210/var/log/messages`（事前にSSHの鍵登録が必要です）

**TWSNMP FC** (v1.4.0～)
`-s`に `twsnmp://192.168.1.250:8080` と指定し、`--api`を指定すれば、Web API経由でログをインポートできます（`--logType`でsyslog以外も指定可能）。

**IMAP / POP3 / EML** (v1.20.0～)
メール連携に対応しました。`-s`に `imap://192.168.1.1` や `pop3s://...` のように指定することで、メールのヘッダをログとして取り込むことができます。Emlファイルの取り込みも直接ファイルを指定するだけです（例: `twsla import sample.eml`）。

**Windows イベントログ（evtx）** (v1.1.0～)
evtxファイルを読み込む時に `--json` を指定すれば、WindowsのイベントログをJSON形式で読み込みます。

**FTP / FTPS** (v2.1.0～)
`ftp://user:pass@host/path/to/log` や `ftps://...` を指定することで、FTPサーバーから直接ログファイルをダウンロードしてインポートできます。

**twlogeye統合（Loki / Elasticsearch / OpenSearch）** (v2.0.0～)
`twlogeye://...` をソースに指定することで、twlogeye経由でGrafana Loki、Elasticsearch、OpenSearchなどの分散ログ基盤から直接ログをインポートできます。

## データストア形式とその他のオプション (v2.0.0～)

ログの保存先データベースは `-d`（または `--datastore`）オプションで指定します（省略時は `./twsla.db`）。指定するファイルの拡張子によって自動的にストレージエンジンが切り替わります。

- **`.parquet` (Apache Parquet)**: 列指向フォーマット。数百万行を超える大規模ログでも圧倒的な圧縮率と高速なクエリ・分析性能を発揮します。
- **`.badger` (Badger)**: 高速なKey-Valueストア。大量データの書き込み・イテレーションに優れています。
- **`.db` (bbolt, デフォルト)**: 軽量で安定した単一ファイル組み込みDB。

```bash
# Parquet形式でインポートする例
$ twsla import -d ./access.parquet access.log.gz
```

また、`--noDelta` を指定すると、タイムスタンプの時間差を取得・保存しないため高速化が見込めます。読み込み速度はログが時系列に並んでいるほど速くなります。
