---
title: "Docker版の停止方法"
---


大量のsyslogや Netflowを受信していて沢山のレポートデータを記録している（DBのサイズが毎日数GB増える）TWSNMP FCがDocker環境で動作している場合には停止する時に注意が必要です。


# 停止する時のコマンド

停止する時は、

```
#docker stop -t 300 twsnmpfc
```

のように停止してください。

:::message alert
300はTWSNMP FCがログやレポートを保存するための待ち時間です。秒単位です。
５分で保存できないような使い方だと何か問題が発生すると思います。
:::


# 理由が気なる人へ
```
#dcoker stop twsnmpfc
```

というコマンドで停止した場合

- DockerがTWSNMP FCにTermninateシグナルを送る
- TWSNMP FCが終了処理を行う（各処理の停止、ログやレポートの保存）
- Dockerが１０秒待ってもTWSNMP FCが終了しないと強制終了する

ということが起こります。未保存のログやレポートのデータ量が多い場合には10秒で保存できないため強制終了が発生します。
保存されないデータが発生するという意味です。docker stopコマンドのヘルプを見ると

```
% docker stop --help

Usage:  docker stop [OPTIONS] CONTAINER [CONTAINER...]

Stop one or more running containers

Options:
 -t, --time int   Seconds to wait for stop before killing it (default 10)
```

のように書いてあります。

# 保存されたか心配な人は
心配な人はDockerで稼働するTWSNMP FCのログを確認してください。バックグランドで動作している場合は

```
#docker logs -f twsnmpfc
```

でログを表示できます。stopコマンドで停止した時には

![](/images/books/twsnmpfc-manual/picture_pc_c33515ff234e95287c27a1079b33456f.png)

のようにtwsnmpfcの停止がログに表示されます。このログに停止にかかった時間も記録されています。
