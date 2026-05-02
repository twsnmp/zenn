---
title: "VMware 監視"
---
# VMware 監視

ESXiホストやvCenterと連携し、仮想環境のリソース使用状況や稼働状態を監視します。

## 1. 概要
VMwareの標準API（vSphere Web Services API）を使用して、物理ホスト（HostSystem）、ストレージ（Datastore）、および仮想マシン（VirtualMachine）のメトリクスを直接取得します。
エージェントレスで、仮想化基盤全体の健全性を把握できます。

## 2. ポーリング設定
- **種別**: `vmware`
- **モード**:
    - `HostSystem`: 物理ホストのリソースを監視します。
    - `Datastore`: データストア（ストレージ）の空き容量を監視します。
    - `VirtualMachine`: 特定のインスタンス（仮想マシン）の状態を監視します。
- **パラメータ**: 監視対象のオブジェクト名（インベントリ上の表示名）。
- **スクリプト**: リソース使用率（%）による判定。

## 3. 取得結果 (PE.Result)

### `HostSystem` / `VirtualMachine` モード
- **`state`**: 稼働状態。 (備考: `connected`, `poweredOn` 等)
- **`cpu`**: CPU使用量 (MHz)。
- **`totalCpu`**: CPU総容量 (MHz)。 (備考: (Hostのみ))
- **`mem`**: メモリ使用量 (MB)。
- **`totalMem`**: メモリ総容量 (MB)。
- **`upTime`**: 起動時間（秒）。

### `Datastore` モード
- **`capacity`**: データストアの総容量。 (単位: Bytes)
- **`freeSpace`**: 空き容量。 (単位: Bytes)
- **`usage`**: 使用率。 (単位: %)

## 4. JavaScript 判定例

### 仮想マシンのメモリ使用率（90%以下）を監視
- **モード**: `VirtualMachine`
- **パラメータ**: `Web-Server-01`
- **スクリプト**: `(mem / totalMem) * 100 < 90`

## 5. 注意点
- **認証**: vCenterまたはESXiのユーザー名・パスワードが必要です。これらは **ノード設定** のログイン情報として定義してください。
- **オブジェクト名**: パラメータに指定する名前は、vSphere Client上での表示名と **完全一致** させる必要があります。
- **負荷**: 大規模なvCenter環境で非常に多くのオブジェクトを短間隔で監視すると、APIセッションの過負荷を招く恐れがあります。適切な間隔（1分以上推奨）を設定してください。
