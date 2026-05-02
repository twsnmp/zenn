---
title: "HTTP(S) サーバー監視"
---
# HTTP(S) サーバー監視

Webサーバーの稼働状態、応答内容、パフォーマンスメトリクスを詳細に監視します。

## 1. 概要
HTTP/HTTPSのGETリクエストを送信し、レスポンスコード、応答時間、ボディの内容を評価します。単なる死活監視だけでなく、ページの改ざん検知や、サーバーの詳細なステータス取得が可能です。

## 2. ポーリング設定
- **種別**: `http`
- **モード**:
    - (空欄): 標準的なGETリクエスト（証明書検証なし）。
    - `https`: 証明書を正しく検証するHTTPSリバースプロキシ等に使用。
    - `hash`: 応答ボディのSHA256ハッシュ値を計算し、変化を監視します。
    - `metrics`: Apache, Nginx, Fiber等のステータス出力ページからメトリクスを抽出します。
- **パラメータ**: 対象のURL（例: `http://192.168.1.1/status`）。
- **抽出 (Extractor)**: ボディから値を抽出するためのエンジンを選択。
- **スクリプト**: 判定ロジック。

## 3. 取得結果 (PE.Result)

- **`code`**: HTTPステータスコード (200, 404, 500等)。
- **`status`**: HTTPステータス文字列 (OK, Not Found等)。
- **`rtt`**: 最初のリクエストから完了までの時間。 (単位: ナノ秒)

### ハッシュモード時の追加変数
- `sha256`: 今回取得したボディのハッシュ値。
- `last_sha256`: 前回取得したハッシュ値。
- `first_sha256`: ポーリング開始時に取得した初回ハッシュ値。

### メトリクスモード時の変数 (自動抽出)
- **Apache**: `BusyWorkers`, `IdleWorkers`, `Total Accesses`, `Total kBytes` など。
- **Nginx**: `active_connectios`, `accepts`, `handled`, `requests` など。
- **Fiber**: `pid_cpu`, `pid_ram`, `os_cpu`, `os_ram`, `os_load_avg` など。

## 4. 抽出エンジン (Extractor)
複雑なページから特定の情報のみを取り出して判定に使用できます。

- **goquery**: jQueryライクなセレクターを使用してHTML要素を抽出。 (例: `goquery("#current_state")`)
- **jsonpath**: JSONレスポンスから値を抽出。 (例: `jsonpath("$.status.load")`)
- **getBody**: レスポンスボディ全体を文字列として取得.
- **Grokパターン名**: 定義済みのGrokを使用してログ形式の応答を解析。

## 5. JavaScript 判定例

### ステータスコードとキーワードの監視
- **抽出**: `getBody`
- **スクリプト**: `code == 200 && getBody().indexOf("Ready") != -1`

### ページ改ざん検知 (hashモード)
- **モード**: `hash`
- **スクリプト**: `sha256 == first_sha256`

### Nginxのリクエスト増分の監視 (metricsモード)
- **モード**: `metrics`
- **スクリプト**: `(requests - requests_last) / interval < 100`

## 6. 注意点
- **リクエストサイズ**: メモリ保護のため、64MBを超えるレスポンスボディは取得できません。
- **タイムアウト**: ネットワーク遅延やサーバーの過負荷を考慮し、適切なタイムアウト値を設定してください。
