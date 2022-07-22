---
title: "Kubernetes環境で使う"
---

TWSNMP FCをKubernetes環境で動かす方法の説明です。とりあえず動かす方法からKubernetesぽく動かす方法まで段階的に説明します。
Docker Desktopに付いているKubernetes環境で簡単に試せます。

![](/images/books/twsnmpfc-manual/1639260619094-0XkmPeP703.png)


# とりあえずKubernetes環境で動かす
まずは、TWSNMP FCがKubernetes環境で動くか試してみる必要があります。そのためには始めから難しいことやらないでKubernetes環境で起動するための最低限の設定で動かしてみます。最小の構成(YAML)ファイル

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: twsnmp
  labels: 
    svc2pod: twsnmp
spec:
  containers:
  - name: twsnmp
    image: twsnmp/twsnmpfc:latest
    ports:
    - name: http
      containerPort: 8080
    env:
      - name: TZ
        value: "Asia:Tokyo"
      - name: TWSNMPFC_PORT
        value: "8080"
    volumeMounts:
    - name: twsnmp-storage
      mountPath: /datastore
  volumes:
  - name: twsnmp-storage
    emptyDir: {}
---
apiVersion: v1
kind: Service
metadata:
  name: twsnmp
spec:
  type: NodePort
  selector:
    svc2pod: twsnmp
  ports:
  - port: 8080
    nodePort: 30080
```
を、

```
% kubectl apply -f twsnmpfc1.yml
pod/twsnmp created
service/twsnmp created
```
のように適用すれば、TWSNMP FCを起動できます。 KubernetesのノードのIPアドレスの30080番ポートにアクセスすれば、

![](/images/books/twsnmpfc-manual/1639260464621-ioyvqn3Gv7.png)

のような画面が表示されるはずです。
最小限の構成ファイルのポイントは、

- TWSNMP FCのコンテナイメージからPODを作る
- /datastoreのディレクトリはemptyDirのボリュームを割り当てる
- NodePortでノードの30080番ポートをPODの8080番ポートに接続する

ということです。

# 最小限に構成ファイルでは物足りないこと

最小限の構成ファイルでTWSNMP FC起動はできますが実用に使うには課題があります。

- syslog,SNMP TRAP,NetFlowが受信できない
- PODを削除するとデータが消えてしまう
- kubernetesぽい起動方法ではない

# syslog/SNMP TRAP/NetFlowを受信できるようにする

syslog/SNMP TRAP/NetFlowを受信できるようにした構成ファイル

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: twsnmp
  labels: 
    svc2pod: twsnmp
spec:
  containers:
  - name: twsnmp
    image: twsnmp/twsnmpfc:latest
    ports:
    - name: http
      containerPort: 8080
    - name: syslog
      protocol: UDP
      containerPort: 514
    - name: snmptrap
      protocol: UDP
      containerPort: 162
    - name: netflow
      protocol: UDP
      containerPort: 2055
    env:
      - name: TZ
        value: "Asia:Tokyo"
      - name: TWSNMPFC_PORT
        value: "8080"
    volumeMounts:
    - name: twsnmpfc-storage
      mountPath: /datastore
  volumes:
  - name: twsnmpfc-storage
    emptyDir: {}
---
apiVersion: v1
kind: Service
metadata:
  name: twsnmp
spec:
  type: NodePort
  selector:
    svc2pod: twsnmp
  ports:
  - port: 8080
    name: http
    nodePort: 30080
  - port: 514
    name: syslog
    protocol: UDP
    nodePort: 30514
  - port: 162
    name: snmptrap
    protocol: UDP
    nodePort: 30162
  - port: 2055
    name: netflow
    protocol: UDP
    nodePort: 32055
```
を適用すれば、

- UDPの30514番ポートでsyslog
- UDPの30162番ポートでSNMP TRAP
- UDPの32055番ポートでNetFlow

を受信できるようになります。

# データを永続化する
すこしづつ使えるようになってきました。次は、PODを削除してもデータが残るようにします。簡単な方法は、PODのVolumeの部分を変えることです。
構成ファイルの

```yaml
    volumeMounts:
    - name: twsnmpfc-storage
      mountPath: /datastore
  volumes:
  - name: twsnmpfc-storage
    emptyDir: {}
```
の部分を
```yaml
    volumeMounts:
    - name: twsnmpfc-storage
      mountPath: /datastore
  volumes:
  - name: twsnmpfc-storage
    nfs:
      server: 192.168.1.203
      path: "/volume1/twsnmp/test1"
  ```
のようにNFSやローカルのボリュームに変えます。私は、NFSサーバー(192.168.1.203)の公開ディレクトリ（/volume1/twsnmp/test1）に割当ました。これでデータストアがNFSサーバー上に作成されるようになります。
もう少しKubernetesぽくデータの永続化をするには、PersistentVolumeと
PersistentVolumeClaimを使います。
PODのvolumeの設定を
```yaml
    volumeMounts:
    - name: twsnmpfc-storage
      mountPath: /datastore
  volumes:
  - name: twsnmpfc-storage
    nfs:
    persistentVolumeClaim:
      claimName: nfs
```
のようにした、PersistentVolumeとPersistentVolumeClaimを追加します。
```yaml
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs
spec:
  capacity:
    storage: 100Gi
  accessModes:
    - ReadWriteOnce
  nfs:
    server: 192.168.1.203
    path: "/volume1/twsnmp/test1"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: ""
  resources:
    requests:
      storage: 100Gi
```

同じNFSサーバーを使ってデータストアが永続化できました。

# Kubernetesぽく起動する
ここまでは、TWSNMP FCのPODを起動していましたが、KubernetesぽくPODを起動しているノードの障害時に他のノードで代替のPOD起動してくれるようにしたくなります。そのためのこれまでの構成ファイルのPODをDeploymentに変えます。変えた構成ファイルは、

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: twsnmp
spec:
  selector:
    matchLabels:
      app: twsnmp
  replicas: 1
  template:
    metadata:
      labels:
        app: twsnmp
    spec:
      containers:
      - name: twsnmp
        image: twsnmp/twsnmpfc:latest
        ports:
        - name: http
          containerPort: 8080
        - name: syslog
          protocol: UDP
          containerPort: 514
        - name: snmptrap
          protocol: UDP
          containerPort: 162
        - name: netflow
          protocol: UDP
          containerPort: 2055
        env:
          - name: TZ
            value: "Asia:Tokyo"
          - name: TWSNMPFC_PORT
            value: "8080"
        volumeMounts:
        - name: twsnmpfc-storage
          mountPath: /datastore
      volumes:
      - name: twsnmpfc-storage
        nfs:
        persistentVolumeClaim:
          claimName: nfs
---
apiVersion: v1
kind: Service
metadata:
  name: twsnmp
spec:
  type: NodePort
  selector:
    app: twsnmp
  ports:
  - port: 8080
    name: http
    nodePort: 30080
  - port: 514
    name: syslog
    protocol: UDP
    nodePort: 30514
  - port: 162
    name: snmptrap
    protocol: UDP
    nodePort: 30162
  - port: 2055
    name: netflow
    protocol: UDP
    nodePort: 32055
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs
spec:
  capacity:
    storage: 100Gi
  accessModes:
    - ReadWriteOnce
  nfs:
    server: 192.168.1.203
    path: "/volume1/twsnmp/test1"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: ""
  resources:
    requests:
      storage: 100Gi
```
です。これを適用すれば、

```
% kubectl apply -f twsnmpfc5.yml
deployment.apps/twsnmp created
service/twsnmp created
persistentvolume/nfs created
persistentvolumeclaim/nfs created
```
のようにDeploymentが作成されます。たぶんノードの障害が発生したら別のノードでPODを作成してくれると思います。

# Kubernetes環境で動かして面白かったこと
TWSNMP FCのARP Watchを有効にすると同じセグメントに接続されているLANデバイス（PCとかネットワーク機器とか）をリストアップすることができます。マップ設定

![](/images/books/twsnmpfc-manual/1639264716712-iBdWZIM73F.png)

のARP Watch設定を有効して、しばらくすると「レポート」ー「デバイス」ー「LANデバイス」に発見したLANデバイスが表示されます。

![](/images/books/twsnmpfc-manual/1639264912354-AtBAvCamnJ.png)

これは、PODネットワーク上のPODのようです。DNSサーバーなどがあります。

# Kubernetesは、まだまだ分からないことだらけ
とりあえずKubernetes環境でTWSNMP FCを起動できました。でも、分からないことが沢山あります。試してみるには沢山時間がかかりそうなので、今回はここまでにしておきます。もう少しKubernetesの勉強をしてから考えようと思います。
今の時点では

- replicasを１ではなく２以上にすれば冗長化になる？
- PODのローリングアップデートは動作するのか？
- syslogなどの送信先を冗長化できないか？

などなど
KuberetesのAPIでノードやPODの情報が取得できるのでTWSNMP　FCのポーリングが管理画面で表示できるようにするアイデアもあります。
これらの情報をsyslogで送信するセンサー（PCAP、Windowsなどと同じ）の開発も考えています。楽しみが増えました。



