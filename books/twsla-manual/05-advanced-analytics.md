---
title: "高度な分析 (tfidf・anomaly・sigma・ai)"
---

# tfidfコマンド

![](/images/twsla/tfidf.png)

TF-IDFを使って、珍しい（レアな）ログを見つけるコマンドです。

```bash
twsla help tfidf
Use TF-IDF to find rare logs.
```

![](https://assets.st-note.com/img/1716675268711-yeoAjdEYAx.png?width=1200)

`-l` で類似度のしきい値、`-c` で許容回数を指定でき、`-n` で結果から珍しい上位N件を取得可能です。

---

# anomalyコマンド

![](/images/twsla/anomaly.png)

ログをAI分析（Isolation Forest）して異常を検知するコマンド（v1.1.0〜）です。

```bash
twsla anomaly [flags]
```

`-m` オプションで検知モードを指定します：
- `tfidf`: TF-IDFでログの特徴ベクトルを作成（デフォルト）
- `sql`, `os`, `dir`: SQLインジェクションやOSコマンドインジェクションに使われるキーワードの頻度から特徴ベクトルを作成
- `number`: ログに登場する数値から特徴ベクトルを作成

数値データの場合は `-e` オプションで読み込む数値の位置を指定できます。
分析結果では「Score」が大きいほど異常として判断され、特にWebサーバーのAccessログで威力を発揮します。

---

# sigmaコマンド

![](/images/twsla/sigma.png)

脅威検知の標準フォーマット [SIGMA (SigmaHQ)](https://sigmahq.io/) のルールを使った検査を行うコマンドです。

```bash
twsla sigma [flags]
```

- `-s` オプションでSigmaルールの保存ディレクトリを指定します。
ログがJSON形式でない場合は、`-g`（GROK定義）や`-x`（パターンの指定）を使ってデータを抽出・マッピングします。
組み込みのWindowsイベントログ用設定などを利用する場合は、`-c windows` と指定すれば、Sigmaルールから自動的にJSONフィールドへの変換が行われます。

結果画面で「検知したルールの情報」を表示し、`Return` キーで対象の元ログを表示できます。`c`キーでルール毎の集計画面、`g`キーでグラフ表示も可能です。

---

# ai コマンド

![](/images/twsla/ai.png)

LLM（大規模言語モデル）と連携してログを自然言語ベースで分析するためのコマンドです。（v1.17.0で大幅強化）

```bash
twsla ai <filter>... [flags]
```

APIキーは環境変数（`GOOGLE_API_KEY`、`ANTHROPIC_API_KEY`、`OPENAI_API_KEY`等）で設定します。ローカルで動作するOllamaの場合はAPIキー不要です。

v1.21.0から、ログ内のPII（個人情報：IP・メール・電話番号等）をAIへ送信する前に「自動的にマスク」するようになりました（不要な場合は `--aiNoMask` ）。

画面でログを選択し `e` キーを押すとAIによる解説が表示され、`a` キーを押すと検索したログ「全体」に関する分析が行われます。
