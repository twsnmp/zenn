---
title: "SNMP 基本"
---
# SNMP 基本

TWSNMPにおけるSNMPポーリングの基本設定と、サポートされている各種モードについて解説します。

## 1. 概要
TWSNMPは、従来のSNMP v1/v2cに加え、セキュアな通信を可能にする **SNMP v3** をフルサポートしています。強力な認証と暗号化により、安全なネットワーク監視を実現します。

## 2. SNMP v3 セキュリティ設定
SNMP v3では、以下のアルゴリズムを組み合わせて利用できます。

- **認証アルゴリズム (Authentication)**: 
  - `MD5`, `SHA`, `SHA224`, `SHA256`, `SHA384`, `SHA512`
- **暗号化アルゴリズム (Privacy)**: 
  - `DES`, `AES`, `AES192`, `AES256` (および各バリエーション)

> [!NOTE]
> 最新のセキュリティ基準に合わせて、`SHA256` 以上および `AES256` の利用を推奨します。

## 3. 自動発見テンプレートの例 (JSON)

以下は、自動発見で使用できる代表的な定義例です。

```json
[
  { "Name": "SNMP再起動監視", "Type": "snmp", "Mode": "sysUpTime", "Level": "low", "Descr": "対象ノードの再起動を検知" },
  { "Name": "インターフェイス監視", "Type": "snmp", "Mode": "ifOperStatus", "Params": "$i", "Level": "low", "AutoMode": "index:ifIndex" },
  { "Name": "SNMP通信量測定", "Type": "snmp", "Mode": "traffic", "Params": "$i", "Level": "off", "AutoMode": "index:ifIndex" },
  { "Name": "CPU平均使用率", "Type": "snmp", "Mode": "stats", "Params": "hrProcessorLoad", "Script": "avg < 90.0", "Level": "low" }
]
```

## 4. JavaScript での高度な判定
ポーリング結果に対して、`otto` (JavaScriptエンジン) を用いた高度な判定が可能です。

### 利用可能なグローバル関数
- `setResult(name, value)`: カスタムの結果を PE.Result に保存します。
- `getResult(name)`: PE.Result から値を取得します。
- `setLevel(level)`: 判定レベル（`normal`, `warn`, `high`, `low`, etc.）を動的に変更します。

### 前回の値の参照
`[変数名]_last` という名前で、前回の取得値を参照できます。
例: `(ifInOctets - ifInOctets_last) / interval > 1000`
