---
title: "delay・time・heatmap・relationコマンド"
---

# delayコマンド

![](/images/twsla/delay.png)

Accessログ（Webサーバー等）から処理の「遅延」を検知するためのコマンド（v1.3.0〜）です。通常、Accessログはリクエストを受け付けた時刻が記録されますが、実際のログ出力は応答後に行われます。大量のダウンロードなどの処理で時間がかかると、より前のリクエストのログが後に現れる「タイムスタンプの逆転現象」が起こります。これを検知して処理遅延を見つけます。

```bash
twsla delay [flags]
```

`-q` オプションに `1` 以上の数値を指定すると、Syslog等に転送されたログ内にある複数のタイムスタンプの時間差を検知するモードになります（0や省略時は逆転検知モード）。

結果画面:
- `Enter` キー: ログの詳細を表示
- `t` キー: 時刻順にソート
- `d` キー: 遅延の大きさ順にソート
- `s` キー: ファイル（画像等）で保存

---

# timeコマンド

ログ間の時間差（記録間隔）を分析するコマンド（v1.6.0〜）です。

```bash
twsla time [flags]
```

![](https://assets.st-note.com/img/1729485261-4NeIF2sytM0lxYwTrnHfikQg.png?width=1200)

`m`キーで基準となるログにマークを付けます。
- **Diff**: マークしたログとの時間差
- **Delta**: 直前のログとの時間差（平均、中央値、最頻値、標準偏差も表示）

HTMLやPNGで保存すると、Deltaを時系列プロットしたグラフが出力されます。

---

# heatmapコマンド

![](/images/twsla/heatmap.png)

曜日または日付単位でログの多い時間帯をヒートマップで視覚化するためのコマンドです。

```bash
twsla heatmap [flags]
```

- `-w` または `--week` オプションで曜日単位の集計を行います。省略時は日付単位です。

![](https://assets.st-note.com/img/1726436714-pUIb1AKFhWPGuxLV2gelzRJM.png?width=1200)

HTMLファイルとして保存すれば、インタラクティブに時間帯の傾向を確認可能なグラフが得られます。

---

# relationコマンド

![](/images/twsla/relation.png)

ログから抽出した2つ以上の項目（例: IPアドレスとMACアドレス）の関係をリストアップし、有向グラフとして出力もできるコマンドです。

```bash
twsla relation <data1> <data2>... [flags]
```

指定可能な項目:
- `ip`: IPアドレス
- `mac`: MACアドレス
- `email`: メールアドレス
- `url`: URL
- `regexp/パターン/`: 正規表現にマッチした文字列

例:
```bash
$ twsla relation -f Failed -r user "regex/user\s+\S+/" ip
```
結果をHTMLで保存(`s`キー)すると、関係を表現するネットワークグラフとして可視化できます。
