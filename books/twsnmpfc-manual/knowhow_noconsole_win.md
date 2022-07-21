---
title: "Windows環境でコンソールウインドウを表示しないで使う方法"
---


TWSNMP FCの起動プログラムを作る前に

>「TWSNMP FC」をWindowsで起動した場合、コマンドプロンプトを誤って閉じるとプログラムが終了するので
> そこが懸念材料となりそうです。

という問い合わせがありました。
起動プログラムを使えば同じことができますが、起動パラメータを細かく設定して起動したい場合
には、ここで説明する方法が役に立つと思います。



# PowerShellのコマンドがスクリプトに

```
Start-Process -FilePath E:\twsnmpfc\twsnmpfc.exe -WorkingDirectory E:\twsnmpfc\ -ArgumentList "--local" -WindowStyle hidden
```

のようにすれば、コンソールウインドウなしで起動できます。

```
 -WindowStyle hidden
```

がポイントです。Start-Processのマニュアルは

https://docs.microsoft.com/ja-jp/powershell/module/microsoft.powershell.management/start-process?view=powershell-7.1

です。

停止する時は、タスクマネージャーから停止できます。

![](/images/books/twsnmpfc-manual/picture_pc_e7a2174793b39104183138ab849f34ec.png)

PowerShellでpsコマンドを実行してプロセス番号を調べてkillコマンドで

![](/images/books/twsnmpfc-manual/picture_pc_d07da31019ec1fa6aaca7019b78070a1.png)

停止できます。

# タスクスケジューラーに設定する

Windows標準のタスクスケジューラーに登録すればパソコンを起動した時に自動で起動することもできます。

:::message alert
起動プログラムにタスクスケジューラーに登録する機能がありますが、
Mictosoft Storeのからインストールした場合に起動できない。
MSIからインストールした場合でも再起動時に自動起動しないなどの問題があります。
手作業で設定したほうがよさそうです。
:::

タスクマネージャーを起動したら「タスクスケジュールライブラリ」のWindowsを選択して操作の「タスクの作成」を実行します。

![](/images/books/twsnmpfc-manual/picture_pc_86499e4e4dd8d476a3d7f2b15e410942.png)

全般の設定で名前や説明を入力します。ログインしない状態でも起動する設定にすることもできます。

![](/images/books/twsnmpfc-manual/picture_pc_ee330c2ea7ff8201668e72897812ccb5.png)

トリガーを新規追加して

![](/images/books/twsnmpfc-manual/picture_pc_849a9ab149959d17783e17d4bbae3a08.png)

スタートアップ時を選択します。
操作の設定は、

![](/images/books/twsnmpfc-manual/picture_pc_64a37e9d1f506c64d39c2c444a1ece47.png)

プログラム/スクリプトにTWSNMP FCの実行ファイルを指定します。
引数を指定することもできます。開始の欄は、作業ディレクトリを指定します。
条件とは必要ないです。
設定したら選択中の項目を＜実行＞をクリックすれば、起動できるはずです。
操作の実行中の全てのタスクを表示で確認して

![](/images/books/twsnmpfc-manual/picture_pc_431fdfb4d9d04fd03213872684fe6596.png)

のようにTWSNMP FCが表示できれば、OKです。


