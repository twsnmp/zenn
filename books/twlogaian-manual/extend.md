---
title: "玄人向けの拡張機能"
---


ログ分析ツールTWLogAIANを分析するログに合わせて拡張するための機能についての説明です。
自分好みのツールにすることができます。


# ログの種類のカスタマイズ

組み込まれているログの種類以外で情報を抽出したい場合にはカスタムタイプを選択します。

![](/images/books/twlogaian-manual/2022-05-24_16-41-21.png)

抽出パターンをGrokの構文で記述します。Grokのパターンは

https://coralogix.com/blog/logstash-grok-tutorial-with-examples/


がわかりやすいと思いました。
このパターンを理解できれば多くのログ分析ツールで応用できるのでログ分析をするエンジニアのスキルアップにつながると思います。
でも、覚える基本は４つだと思っています。

1. %{パターン:変数名}で情報を抽出する設定
2. ログの中で特徴的な文字列はそのまま残す
3. \s+で区切りのスペースの部分を指定
4. .+で可変の文字列を無視する

TWLogAIANではGrokパターンをできるだけ簡単に作成できる機能を付けています。
ログ分析の設定画面の＜抽出テスト＞ボタン

![](/images/books/twlogaian-manual/2022-05-24_16-43-21.png)

をクリックするとGrokパターンをテストする画面が表示されます。

# 抽出テスト

抽出テスト画面は

![](/images/books/twlogaian-manual/2022-05-24_16-44-12.png)

のような感じです。

## テンプレート

組み込まれているログ種類のGrokパターンを読み込みます。

![](/images/books/twlogaian-manual/2022-05-24_16-44-55.png)

## 抽出パターン

抽出パターンを編集する部分です。

![](/images/books/twlogaian-manual/2022-05-24_16-45-53.png)

入力エリアで編集すると下段の色分けした表示が更新されます。
色分けは黄色が抽出する変数、青がスペース、赤が無視する部分です。
編集エリアにログをコピーして範囲を選択してTabキーを押せば適切な抽出パターンに変換します。

![](/images/books/twlogaian-manual/picture_pc_a56a1a967b4a236795515fa95a7f05ca.gif)

のような感じです。変数の名前を適当に変えます。
選択してESCキーを押せば、無視する部分に指定できます。

## テストデータ

編集したGrokの抽出パターンをテストするためのログをコピペするエリアです。

## ＜自動抽出パターン生成＞ と ＜AIパターン生成＞ (v2.1.0)

テストデータの１行目のログを解析して自動でパターンを作成する「自動抽出パターン生成」に加え、v2.1.0より**「AIパターン生成」**に対応しました。

![](/images/books/twlogaian-manual/grok_ai_generate.png)

テストデータに実際のログを貼り付け、＜AIパターン生成＞ボタンをクリックすると、AI（LLM）がログの構造を推論し、タイムスタンプやIP、ホスト名、セベリティ、可変メッセージなどを適切に抽出するGrokパターンを自動で組み立てます。手動で細かく正規表現を記述する手間が大幅に削減されます。

## ＜終了＞ボタン

編集したパターンを破棄して抽出テストの画面を終了します。

## ＜適用＞ボタン

編集したパターンを設定画面の抽出パターンに適用して抽出テストの画面を終了します。

## ＜テスト＞ボタン

編集したGrok抽出パターンをテストします。テストデータのログから情報を抽出できるか試すということです。
実行すると

![](/images/books/twlogaian-manual/2022-05-24_16-49-54.png)

のような感じです。

抽出できない行があると上部にエラー表示されます。
下の方に抽出した結果を表示します。名前が定義されていない変数は赤い時で表示されます。
エラーがなくなり目的の情報を抽出できるようになるまでパターンを編集します。根気のいることです。

# 抽出パターン、変数名のエクスポート

編集した抽出パターンでインデックスを作成した後、検索画面のエクスポートからログ種別定義

![](/images/books/twlogaian-manual/2022-05-24_16-51-34.png)

を実行すると設定をファイルに保存できます。

# ログ種別定義ファイル

yaml形式なのでテキストエディターで編集できます。

```yaml
extractortypes:
- key: custom_20220307065138
  name: TCP接続数
  grok: '%{TIMESTAMP_ISO8601:timestamp}\s+(?:%{SYSLOGFACILITY} )?%{SYSLOGHOST:logsource}\s+%{NOTSPACE:tag}:\s+.*sce=%{INT:sce}.*'
  timefield: timestamp
  ipfields: ""
  macfields: ""
  view: ""
fieldtypes:
- key: sce
  name: 有効なTCP接続数
  type: number
  unit: "件"
```

のようなファイルです。

extractortypesがログの定義です。
keyが定義の識別する値です。nameは人間のための名前、grokがパターンです。
tilefieldがタイムスタンプとして認識する変数名、ipfiledsがIPアドレスとしてホスト名検索、位置情報検索に使う変数名です。
macfieldsがMACアドレスからベンダー名を検索するために使用する変数名です。

fieldtypesが変数の定義です。
keyが変数名です。nameが人間のための名前、typeが変数の型です。
数値(number)か文字列(string)を指定します。
unitはグラフに表示する単位です。

# ログ種別定義のインポート

ログ分析の設定画面の下の方にある＜ログ定義インポート＞ボタン

![](/images/books/twlogaian-manual/2022-05-24_16-54-04.png)

でログ種別定義ファイルをインポートできます。

```yaml:apacheErrorLog.yaml
extractortypes:
- key: APACHE_ERROR
  name: Apacheエラーログ
  grok: \[%{GREEDYDATA:timestamp}\] \[%{WORD:level}\]\s+(?:\[client\s+%{IPV4:client}\]\s+)?%{GREEDYDATA:message}
  timefield: ""
  ipfields: ""
  macfields: ""
  view: ""
```

のファイルをインポートすればログの種類の選択肢に

![](/images/books/twlogaian-manual/2022-05-24_16-56-50.png)

のように追加されます。

この様な定義ファイルを作って配布すれば、特殊なログの分析に役に立つと思います。

---

# Sigma CLIツール機能 (v2.2.0)

TWLogAIANの実行バイナリは、ターミナルから引数を指定して実行することで、Sigmaルールのテストやデータストアに対するバッチスキャン、Wazuhルール変換を行えるCLIツールとしても利用できます。

```bash
# 組み込みルールパック一覧の確認
twlogaian sigma list

# 単一ログに対するルールマッチングテスト
twlogaian sigma test -p linux-auth -l "Failed password for invalid user admin from 192.168.1.50 port 22 ssh2"

# 保存したParquetデータストアに対するSigma一括スキャン
twlogaian sigma scan -d ./datastore.parquet -p windows-ad,network-threats

# Wazuh XMLルールファイルをSigma形式（YAML）に一括変換
twlogaian sigma wazuh2sigma -i /var/ossec/rules/ -o ./sigma-rules/
```




