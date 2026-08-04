---
title: "LLM・AI連携機能"
---

# LLM・AI連携機能の概要

TWSNMP FK v2.0.0 以降では、大規模言語モデル（LLM）と連携したAIアシスタント機能が搭載されています。
ネットワーク障害の診断、難解なログメッセージの解釈、ポーリング監視項目の自動生成、各種レポートの傾向要約など、ネットワーク管理者の運用負担を軽減するための各種AI支援が利用可能です。

---

# LLMの設定

AI機能を利用するには、あらかじめ設定画面でLLMプロバイダーと接続情報を設定する必要があります。

![TWSNMP FK LLM設定画面](https://raw.githubusercontent.com/twsnmp/twsnmpfk/main/docs/images/ja/llm_setting.png)

## 設定項目

| 項目 | 内容 |
| ---- | ---- |
| **LLMプロバイダー** | 利用するLLMサービスを選択します（OpenAI, Gemini, Claude, Ollama など）。 |
| **エンドポイント (URL)** | APIエンドポイントを指定します。Ollamaの場合は `http://localhost:11434` を指定します。 |
| **モデル名** | 使用するモデル名（例: `gpt-4o`, `gemini-1.5-pro`, `claude-3-5-sonnet-200000`, `gpt-oss` など）。 |
| **APIキー** | クラウドプロバイダー利用時に必要なAPIキー。ローカルLLM（Ollama）の場合は空欄で可。 |
| **システムプロンプト** | 必要に応じてAIへの共通インストラクションを調整できます。 |

:::message
**ローカルLLM（Ollama）の活用**:
社内ネットワークのIPアドレスやログ情報を外部クラウドに送信したくない場合は、Ollamaプロバイダーと `gpt-oss` 等のローカルモデルを組み合わせることで、完全ローカル・オフライン環境で安全にAI機能を利用できます。
:::

---

# AIアシスタント機能一覧

## 1. ノードAI総合診断

ノードの詳細画面またはマップ上のノード操作から「AI診断」を実行できます。

* **診断内容**:
  ノードの基本情報（IP/MAC/SNMP情報）、設定されているポーリングの稼働状態、および過去24時間以内に発生した関連ログ（Syslog, SNMP Trap, EventLog, ARP等）を総合的に判定します。
* **出力結果**:
  現在のノード状態に対する原因推測、ネットワークへの影響度、および管理者として推奨される確認・対処手順が日本語で出力されます。

![ノードAI総合診断画面](https://raw.githubusercontent.com/twsnmp/twsnmpfk/main/docs/images/ja/node_ai_diag.png)

---

## 2. 個別ログのAI解説

Syslog、SNMP TRAP、EventLog などのログ閲覧画面において、各ログの「AI解説」ボタンをクリックすることで実行できます。

* エラーコードや専門的なシステムログの意味を分かりやすく日本語で要約・解説します。
* ログが発生した背景要因や、確認すべき箇所（ポート、設定ファイル、関連サービスなど）を提示します。

---

## 3. Syslog / イベントログからのポーリング作成AIアシスト

受信したSyslogメッセージを選択し、「AIからポーリング追加」を実行することで、該当ログを継続監視するためのポーリング設定を自動生成します。

* **正規表現抽象化**: PIDやポート番号、送信元IPなど毎回変わる可変部分をAIが識別し、汎用的な正規表現フィルター（Filter）を構成します。
* **判定スクリプト生成**: TWSNMP FKのJavaScript判定仕様（正常時に `true` または `count == 0`）を満たす評価式を自動生成します。

![Syslogからのポーリング作成AIアシスト](https://raw.githubusercontent.com/twsnmp/twsnmpfk/main/docs/images/ja/syslog_polling_ai.png)

---

## 4. レポート画面のAI要約・解説

Syslog、SNMP TRAP、NetFlow/sFlow、Polling、IPアドレス、ARPなどの各レポート画面に「AI解説」ボタンが配置されています。

* **傾向の集計**: 発生件数の変化スパイクや主要な送信元ホストの抽出。
* **重要度の判定**: 異常なログイン試行やトラフィック急増などの兆候を分析。
* **対処ガイド**: 集計結果から管理者が優先して対応すべきアクションの提示。

![レポート画面のAI要約解説](https://raw.githubusercontent.com/twsnmp/twsnmpfk/main/docs/images/ja/report_ai_summary.png)

---

## 5. 自然言語によるポーリング作成アシスト

ポーリング一覧画面から新規ポーリングを作成する際、「AIアシスト」ダイアログを利用できます。

* **自然言語入力**: 「Pingの応答時間が100msを超えたらアラート」「Webサーバーのレスポンスコードが200以外なら異常」といった日本語の文章で指示を与えます。
* **自動変換**:
  * ポーリング種別（`ping`, `http`, `snmp` など）の決定
  * 単位の適合（Pingのナノ秒単位計算など）
  * 判定スクリプトの作成
  * 関連するSNMP MIB名・OIDの自動検索

![AIポーリング作成アシスト画面](https://raw.githubusercontent.com/twsnmp/twsnmpfk/main/docs/images/ja/polling_assist_modal.png)
