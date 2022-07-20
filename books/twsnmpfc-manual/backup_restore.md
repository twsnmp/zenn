---
title: "リストア"
---

リストアは、バックアップしたデータベースファイルを/datastore/twsnmpfc.dbへコピーすれよいです。
しかし、稼働中のTWSNMP FCのコンテナにコピーすると開いた状態にデータベースファイルに上書きすることになるのでよくありません。
alpineなどの他のLinuxのイメージでコンテナを作って/datastoreをマウントしてコピーするようなことが必要です。
そこで、データベースファイルを移動する方法にも使えるリストア機能を作りました。

まずは、空のデータベースで起動します。

```
#docker run --rm -d --name twsnmpfc --net host -v twsnmpfc:/datastore twsnmp/twsnmpfc
```
この状態でバックアップのディレクトリを作成します。
```
#docker exec -it twsnmpfc mkdir /datastore/backup
```
このバックアップのディレクトリに使いたいデータベースファイルをコピーします。稼働中のデータベースファイルではないので上書きにはなりません。

```
#docker cp /tmp/twsnmpfc.db twsnmpfc:/datastore/backup/
```
一度、コンテナを停止します。
```
#docker stop twsnmpfc
```
リストアコマンドでデータベースファイルを入れ替えます。リストアコマンドはデータベースを開かずに入れ替えるだけです。

```
#docker run --rm -it --name twsnmpfc --net host -v twsnmpfc:/datastore twsnmp/twsnmpfc -restore twsnmpfc.db
2021/05/22 07:02:04 restore done
```

この後、コンテナを起動すれば、コピーしたデータベースファイルで起動します。
バックアップも/datastore/backupに保存するので、
```
# docker exec -it d1 ls -lh /datastore/backup
total 3G
-rw------- 1 root root 256.0K May 22 06:11 twsnmpfc.db.20210522061144
-rw------- 1 root root 2.7G May 22 06:18 twsnmpfc.db.20210522061204
```
のコマンドで確認できます。リストアコマンドのパラメータにバックアップファイルの名前を指定すれば指定したデータベースファイルに戻すことができます。
リストアする前に使っていたデータベースファイルは、バックアップに移動するので間違っても戻すことができます。

