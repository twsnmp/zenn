---
title: "はじめに・インストール"
---

# はじめてのTWSNMP FK

日本で定番のSNMPマネージャー復刻版です。

## はじめに

TWSNMPは日本で25年以上定番のSNMPv3に対応したSNMPマネージャです。
これを2023年の技術で復刻したのがTWSNMP FKです。
コンテナで動作するTWSNMP FCはWebブラウザーからアクセスして操作しますが、FKは、デスクトップアプリであるためブラウザーは不要です。

## Windows版Microsoft Store

Windows版は[マイクロソフトストア](https://www.microsoft.com/store/apps/9NSQN46P0MVL)で購入できます。

![](/images/twsnmpfk/2023-11-24_15-37-20.png)

## Scoop

[SCOOP](https://scoop.sh/)を参照してScoopをインストール後に、以下のコマンドでインストールできます。

```bash
> scoop bucket add twsnmp https://github.com/twsnmp/scoop-bucket
> scoop install twsnmpfk
```

## Mac OS版のApp Store

Mac版は[Apple App Store](https://apps.apple.com/jp/app/twsnmpfk/id6468539128)で購入できます。

無料で使いたい人は、[GitHUBのリリース](https://github.com/twsnmp/twsnmpfk/releases)からパッケージをダウンロードできます。

![](/images/twsnmpfk/2023-11-24_15-40-18.png)

## Linux版

[GitHubのリリース](https://github.com/twsnmp/twsnmpfk/releases)からパッケージ（`.tar.gz`形式）をダウンロードできます。

### Linux環境での起動と注意点
一般ユーザーとして実行すると、ICMP監視（RAWソケット）や特権ポート（514, 162等）の使用権限がないためエラーになります。
**`sudo` で直接アプリを実行しないでください**（GUIの表示サーバーと接続できなくなる場合があります）。

1. **特権の付与**:
   ```bash
   sudo setcap 'cap_net_bind_service,cap_net_raw+ep' ./twsnmpfk
   ```
2. **ARP監視ツールのインストール** (`arp`コマンドの追加):
   ```bash
   sudo apt-get update && sudo apt-get install -y net-tools
   ```
3. **一般ユーザーとしての起動**:
   ```bash
   ./twsnmpfk
   ```

