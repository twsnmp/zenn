---
title: "Microsoft Store版のタスクスケジューラ登録"
---

Microsoft Store版をタスクスケジューラーに登録して起動できない問題の対処方法です。
Windows環境のtwWinlogなどのセンサーが動作していないことに気づいて、タスクスケジューラーによる起動に失敗しているのかと思って確認してみると初めてみる[アクセスが拒否」というエラーで起動されていませんでした。＜実行＞ボタンを何度押しても状況は変わらずです。
タスクスケジューラーから起動するチェックを外せば問題なく起動できます。

![](/images/books/twsnmpfc-manual/1656797453520-n7gAQILySg.png)

タスクスケジューラーから起動した時だけでだめなようです。
タスクスケジューラーから起動するコマンドをPowerShellで確認すると

![](/images/books/twsnmpfc-manual/1656797263303-GF1CdDzXhA.png)

同じエラーが出ています。実行ファイルを起動できません。

表示されているエラーの
```
NativeCommandFailed
```
をGoogleさんに聞いてみるとありました。
https://seesaawiki.jp/w/kou1okada/d/20220215%3A%20WindowsApps%20%B0%CA%B2%BC%A4%CE%20.exe%20%A4%AC%BC%C2%B9%D4%A4%C7%A4%AD%A4%CA%A4%A4

**WindowsApps 以下の .exe が実行できない**

という同じ問題でした。
この人と同じように実行ファイルをWindowsApps配下から別のディレクトリにコピーして実行してみました。ちゃんと動きました。

![](/images/books/twsnmpfc-manual/1656797846422-agYTveGd0t.png)

タスクスケジューラーの登録する実行ファイルのコピーしたものに変更すれば、こちらも動きました。

![](/images/books/twsnmpfc-manual/1656797928662-UUjKVKhuNT.png)


