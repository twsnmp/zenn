---
title: "search・count・extractコマンド"
---

# search コマンド

![](/images/twsla/search.png)

ログのインポートが完了したら、検索を行うことができます。

```bash
twsla help search
Search logs.
Simple filters, regular expression filters, and exclusion filters can be specified.

Usage:
  twsla search [flags]
```

シンプルフィルター（ `-f` ）、正規表現のフィルター（ `-r` ）、や時間範囲（ `-t` ）を指定してログを絞り込むことができます。最新バージョンでは引数でシンプルフィルターを指定でき、`^` から始めると反転（除外）フィルターになります。

```bash
$ twsla search -f fail
```

![](https://assets.st-note.com/img/1716672574781-gcWleWK4jC.png?width=1200)

検索結果画面の右上にはキー入力ヘルプが表示されます。
- `s` キー: 結果を保存
- `r` キー: 表示を逆順にする
- `q` キー: 終了

**カラー表示機能 (-c, --color)**
v1.5.0から、ログの検索結果をキーワードや正規表現でカラー表示できるようになりました。
例: `twsla search -f Failed -c "regex/user\s+\S+/9,ip,filter"`
画面上から `c` や `m` キーを使用してインタラクティブにマーカーを設定することも可能です。

---

# count コマンド

![](/images/twsla/count.png)

ログの件数を時間単位に集計したり、ログの中のデータをキーとして集計できるコマンドです。

```bash
$ twsla help count
Count the number of logs.
...
Usage:
  twsla count [flags]
```

**時間単位の集計**
抽出データ（`-e`）を指定しない場合は時間単位でログの件数を集計します。
```bash
$ twsla count -f fail
```
集計間隔は `-i` オプションで秒指定でき、省略された場合は自動設定されます。

結果画面では、前のログとの時間差(Delta)も表示され、`c`キーで件数順、`k`キーで時間順にソート可能です。

**グラフの出力**
結果画面で `s` キーを押し、拡張子を `png` や `html` にすると、集計結果のグラフ（静止画やインタラクティブグラフ）を保存できます。

---

# extract コマンド

![](/images/twsla/extract.png)

ログから特定のデータを抽出・抽出結果を時系列に一覧表示するためのコマンドです。

```bash
$ twsla help extract
...
Usage:
  twsla extract [flags]
```

`search` や `count` と同じくフィルターを指定可能です。`-e` オプションで抽出するデータのパターンを指定します。
例:
```bash
$ twsla extract -f fail -e ip
```

![](https://assets.st-note.com/img/1716674893720-WqYN0wwrvt.png?width=1200)

結果表示画面で `i` キーを押すと抽出された数値データの統計情報が表示され、`s` キーでCSV保存やグラフ保存（png/html）が可能です。
