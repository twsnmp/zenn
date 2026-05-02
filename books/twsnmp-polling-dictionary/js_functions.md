---
title: "JavaScript 関数"
---
# JavaScript 関数

TWSNMP FCのポーリング判定スクリプト（JavaScript）内で利用可能な共通関数について解説します。

## 1. setResult
`setResult` 関数は、ポーリング結果（`PE.Result`）に独自の数値や文字列を保存するために使用されます。
保存された値は、ポーリング結果の履歴として記録されるほか、次回以降のポーリングで `[変数名]_last` や `getResult` を通じて参照したり、グラフ表示の対象にしたりすることができます。

### 使い方
```javascript
setResult(name, value)
```
- **`name`**: 保存する変数名（文字列）。
- **`value`**: 保存する値（数値、文字列、または真偽値）。
    - 数値：そのまま浮動小数点数として保存されます。
    - 文字列：そのまま保存されます。
    - 真偽値：`true` は `1`、`false` は `0` として保存されます。

### 使用例
#### 独自の計算結果を保存する
取得した複数のMIB値から算出された値を、新しい指標として記録します。
```javascript
var usage = (hrStorageUsed / hrStorageSize) * 100;
setResult("usage_percent", usage);
usage < 90.0;
```

---

## 2. getResult
`getResult` 関数は、ポーリング結果（`PE.Result`）に格納されている値を取得するために使用されます。

### 使い方
```javascript
getResult(name)
```
- **`name`**: 取得したい変数名（文字列）。
- **戻り値**: 格納されている値。存在しない場合は `undefined` を返します。

---

## 3. setLevel
`setLevel` 関数は、ポーリングの判定状態（レベル）をJavaScriptから直接指定するために使用されます。

### 使い方
```javascript
setLevel(level)
```
- **`level`**: 設定したい状態レベル（文字列）。以下のいずれかを指定します。
    - `"normal"`: 正常（緑）
    - `"warn"`: 警告（黄）
    - `"high"`: 重度障害（赤）
    - `"low"`: 軽度障害（茶）
    - `"off"`: 監視停止（灰）

---

## 4. saveReport
`saveReport` 関数は、ポーリングで取得・解析したデータを TWSNMP FC 内部の「レポート」として登録するために使用されます。

### 使い方
```javascript
saveReport(type, data)
```
- **`type`**: レポートの種類（文字列）。
    - `"env"`: 環境センサーレポート（温度、湿度など）
    - `"user"`: ユーザーレポート（ログイン活動など）
    - `"lan"`: デバイスレポート（MAC/IPアドレス帳）
- **`data`**: レポートの内容（JavaScriptオブジェクト）。種類ごとに必要なフィールドが異なります。
- **戻り値**: 登録に成功すれば `true`、失敗すれば `false`。
