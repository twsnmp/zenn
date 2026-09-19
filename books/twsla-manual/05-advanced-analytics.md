---
title: "高度な分析 (tfidf・anomaly・sigma・model・ai)"
---

# tfidfコマンド

![](/images/twsla/tfidf.png)

TF-IDFを使って、ログ集合の中から珍しい（レアな・外れ値）ログを自動発見するコマンドです。

```bash
twsla tfidf [flags]
```

ログ全体の単語・トークン出現頻度から特徴ベクトルを算出し、全対類似度行列（$S = X \cdot X^T$）を計算します。
v2.0.0以降、**GPU（Metal / WebGPU）および SIMD（AVX2）による行列積アクセラレーション**に対応しており、数万件規模のログでも高速に比較・分析されます。

- `-l` または `--limit`: 類似度のしきい値（デフォルト `0.5`）
- `-c` または `--count`: 許容出現回数（指定値以下のレアログを抽出）
- `-n` または `--top`: 珍しいログの上位N件を取得
- `--noGPU`: GPUアクセラレーションを無効化し、CPU/SIMDモードで実行

![](https://assets.st-note.com/img/1716675268711-yeoAjdEYAx.png?width=1200)

---

# anomalyコマンド

![](/images/twsla/anomaly.png)

多彩な機械学習・統計アルゴリズムを用いてログの異常を検知するコマンドです。

```bash
twsla anomaly [flags]
```

### 特徴抽出モード (`-m, --mode`)
ログからどのような数値を抽出してベクトル化するかを指定します：

| モード | 説明 |
|---|---|
| `tfidf` (デフォルト) | ログのトークンからTF-IDFベクトルを作成し、珍しいパターンのログを検知 |
| `sql` | SQLインジェクション攻撃に特有のキーワード頻度を特徴量化 |
| `os` | OSコマンドインジェクション攻撃特有のキーワード頻度を特徴量化 |
| `dir` | ディレクトリトラバーサル攻撃特有のパターンを特徴量化 |
| `walu` | Webアクセスログ統合モード（ステータスコード、メソッド、レイテンシ、パス等を複合評価） |
| `number` | ログ内の数値を抽出して特徴量化（`-e` オプションで抽出パターンを指定） |

### 異常検知アルゴリズム (`-a, --algo`)
用途やデータの性質に合わせてアルゴリズムを選択できます：

| アルゴリズム | 種別 | 説明 |
|---|---|---|
| `iforest` (デフォルト) | 機械学習 | **Isolation Forest**。木構造を用いて孤立しやすい外れ値ログを高速に検知 |
| `autoencoder` | ディープラーニング | **Autoencoder**。組み込み推論エンジン（tensai）による再構成誤差を用いた異常検知 |
| `lstm` | ディープラーニング | **LSTM**。時系列の遷移順序や連続性の異常を検知 |
| `lof` | 機械学習 | **Local Outlier Factor**。密度ベースで局所的な外れ値を検出 |
| `knn` | 機械学習 | **k-Nearest Neighbor**。近傍距離に基づく外れ値検知 |
| `mahalanobis` | 多変量統計 | **マハラノビス距離**。複数変数の共分散を考慮した統計的異常検知 |
| `zscore` | 統計 | **Z-Score**。標準偏差からの乖離に基づく基本的な統計的検知 |

> [!TIP]
> 演算はGPUおよびSIMDによって高速化されています。リソース制限環境では `--noGPU` を指定してCPU実行に切り替えることも可能です。

---

# sigmaコマンド

![](/images/twsla/sigma.png)

脅威検知のデファクトスタンダード [SIGMA (SigmaHQ)](https://sigmahq.io/) のルールを用いてログを検査し、サイバー攻撃や不審な挙動を検知するコマンドです。

```bash
twsla sigma [flags]
```

### 1. 75種類の組み込みルールパック内蔵
外部からルールファイルをダウンロードしなくても、**11種類・合計75ルールの厳選ルールパック**がバイナリに標準組み込みされています。

```bash
# 内蔵ルールパックの一覧を表示
twsla sigma packs

# ルール総数、対応ログソース、MITRE ATT&CK / 規格タグの統計を表示
twsla sigma stat
```

- `-p, --sigmaPacks`: 適用するパックを指定（例: `-p windows-essential,linux-auth`）
- `-s, --rules`: 外部の独自Sigmaルールディレクトリを指定（内蔵ルールと同名IDの場合は外部ルールが自動オーバーライド）
- `-c, --config`: フィールドマッピング設定（`windows`, `linux`, `network`, `web` 内蔵）
- `--strict`: 厳格なルール構文チェックを有効化

また、短時間の連続認証失敗などを捉える**スライディングウィンドウによる相関検知**（時間枠内の条件達成判定）も自動的に処理されます。

### 2. インタラクティブUIの操作
`twsla sigma` を実行すると専用のTUIビューアが起動します：

- `Enter` キー: 該当ログの詳細を展開表示
- `c` キー: **イベント一覧 ⇄ ルール別集計 ⇄ タグ別集計（MITRE ATT&CK / コンプライアンス規格）** を順次切り替え
- `g` または `h` キー: 現在の集計結果をグラフ化（ブラウザまたはSixel/PNG）
- `s` キー: 検知結果や集計結果をファイルに保存

### 3. CLIサブアクションとWazuh連携
Sigmaルールの単体テストや、Wazuh XMLルールの変換もCLIから直接実行できます：

```bash
# 有効なルール一覧の確認
twsla sigma list -p linux-auth

# 単一ログに対するルールマッチングテスト
twsla sigma test '{"content":"Failed password for invalid user admin from 192.168.1.100 port 45678 ssh2"}'

# Wazuh ルール XML から Sigma YAML への一括変換
twsla sigma convert-wazuh -o ./converted-rules ./ruleset/rules/0095-sshd_rules.xml

# Wazuh デコーダー XML から正規表現パターンへの変換
twsla sigma convert-wazuh-decoder -o ./captures ./0310-ssh_decoders.xml
```

---

# model コマンド

組み込みAI分析で使用するローカルLLMモデルをダウンロード・管理するコマンドです。

```bash
twsla model [command]
```

### サブコマンド
- `status`: モデルの保存先ディレクトリおよびハードウェアアクセラレーション（GPU/CPU）の状態を表示
- `download-gpu`: GPU推論を有効化するための `wgpu-native` ライブラリ（Metal / Vulkan / D3D12）を自動ダウンロード
- `presets`: 利用可能なプリセットモデル一覧を表示
- `download <preset|URL>`: プリセット名またはHugging FaceのGGUFモデルURLを指定してダウンロード
- `list` (または `ls`): ダウンロード済みのローカルモデル一覧を表示
- `remove <preset|file>` (または `rm`): ローカルモデルを削除

### 主なプリセットモデル
| プリセット名 | モデル | サイズ目安 | 特徴・推奨用途 |
|---|---|---|---|
| `qwen2.5-coder-0.5b` | Qwen2.5-Coder-0.5B-Instruct | 約500MB | ログ・JSON・コード構造解析に最適（推奨） |
| `qwen2.5-0.5b` | Qwen2.5-0.5B-Instruct | 約500MB | 標準軽量モデル |
| `qwen2.5-1.5b` | Qwen2.5-1.5B-Instruct | 約1.0GB | 高精度な汎用モデル |
| `smollm2-135m` | SmolLM2-135M-Instruct | 約145MB | 超軽量・高速（IoTや最小環境向け） |
| `deepseek-r1-1.5b` | DeepSeek-R1-Distill-Qwen-1.5B | 約1.1GB | `<think>` 思考プロセスを持つ推論型モデル |

```bash
# GPUアクセラレーションのセットアップ
$ twsla model download-gpu

# 推奨のログ解析特化モデルを取得
$ twsla model download qwen2.5-coder-0.5b

# モデル状態の確認
$ twsla model status
```

---

# ai コマンド

![](/images/twsla/ai.png)

LLM（大規模言語モデル）と連携してログを自然言語ベースで詳細に分析・要約するコマンドです。
組み込み推論エンジン [tensai](https://github.com/mattn/tensai) を内蔵しており、**外部APIやOllamaサーバーがなくてもローカル完結でAI分析**を実行できます。

```bash
twsla ai <filter>... [flags]
```

### プロバイダとモデルの指定
- `--aiProvider`: `tensai` (組み込み), `ollama`, `gemini`, `openai`, `claude` を指定可能。
- `--aiModel`: モデル名またはプリセット名（例: `qwen2.5-coder-0.5b`）を指定。
- `--noGPU`: GPUを使用せずCPU/SIMDモードで推論を実行。
- `--aiNoMask`: PII自動マスクを無効化。

> [!NOTE]
> **プロバイダの自動フォールバック順序:**
> 1. ローカルモデル（`~/.twsla/models/`）が存在する場合は、自動的に内蔵の `tensai` を使用
> 2. ローカルモデルがない場合、環境変数（`OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `GOOGLE_API_KEY`）を検索
> 3. APIキーも見つからない場合はローカルの `ollama` にフォールバック

### 個人情報（PII）の自動マスキング
セキュリティ対策として、ログに含まれるIPアドレス、メールアドレス、電話番号などの個人情報は、**AIに送信される直前に自動で難読化・マスク**されます（安全に外部LLMを利用可能）。

### 画面操作
検索結果画面から直感的にAIを呼び出せます：
- `e` キー: 選択した単一ログの詳しい原因や影響をAIが解説
- `a` キー: 検索されたログ「全体」の傾向・異常パターンのサマリーをAIが一括分析
- 分析結果はセッション中キャッシュされ、素早く再確認できます。

