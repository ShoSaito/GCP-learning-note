


# GCEで自動スケーリングを実現する
2021/04/29

## やりたいこと
1. インスタンステンプレートを作成する
2. インスタンステンプレートを利用して、マネージドインスタンスグループを作成する
3. httpロードバランサーを設定する
4. 負荷テストを実施して、インスタンスが自動スケーリングすることを確認する

上記をなるべくコマンドで実行していきます。

## 1. インスタンステンプレートを作成する
基本のコマンドに必要なオプションをつけて実行する。

apacheのインストール時にバージョンを明記するのが実用的
```
gcloud compute instance-templates create template-my-web-server \
    --image-family debian-10 \
    --image-project debian-cloud \
    --tags http-server \
    --machine-type f1-micro \
    --metadata startup-script='#! /bin/bash 
    sudo apt update
    sudo apt -y install apache2=2.4.38-3+deb10u4'
```

下記、正しくないかもしれないが、debianの使い方
```
- パッケージのインストール状況の確認
    - `dpkg -L <pachagename>`

- 利用可能なバージョンの確認
    - `apt-cache showpkg <pachagename>`
```


createコマンドの結果をリストして確認
```
gcloud compute instance-templates list

NAME                    MACHINE_TYPE   PREEMPTIBLE  CREATION_TIMESTAMP
template-my-web-server  f1-micro                    yyyy-mm-ddT03:51:48.531-07:00
```

## 2. インスタンステンプレートを利用して、マネージドインスタンスグループを作成する

マネージドインスタンスグループの作成コマンド
```bash
gcloud compute instance-groups managed create my-vm-group \
    --size 2 \
    --template template-my-web-server \
    --zone asia-northeast1-a
```
パラメタ | 意味　　
-----|---
--size | グループの初期インスタンス数。整数を指定。今回は2
--template | 使用するテンプレート 
--zone | デフォルトから変更がなければ指定は不要?

作成結果の確認
```
gcloud compute instance-groups list

NAME         LOCATION           SCOPE  NETWORK  MANAGED  INSTANCES
my-vm-group  asia-northeast1-a  zone   default  Yes      0
```

インスタンスの確認
```
gcloud compute instances list


NAME              ZONE               MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP    EXTERNAL_IP    STATUS
my-vm-group-xxx1  asia-northeast1-a  f1-micro                   [INTERNAL_IP]  [EXTERNAL_IP]  RUNNING
my-vm-group-xxx2  asia-northeast1-a  f1-micro                   [INTERNAL_IP]  [EXTERNAL_IP]  RUNNING
```

webサーバーの動作確認、返答があればOK
```
curl [EXTERNAL_IP]@my-vm-group-xxx1
curl [EXTERNAL_IP]@my-vm-group-xxx2
```

上記でマネージドインスタンスグループが構成出来た。

## 3. httpロードバランサーを設定する



## 4. 負荷テストを実施して、インスタンスが自動スケーリングすることを確認する





## 公式doc

#### 1. インスタンステンプレートを作成する
[既存のインスタンスに基づくインスタンス テンプレートの作成](https://cloud.google.com/compute/docs/instance-templates/create-instance-templates?hl=ja#based-on-existing-instance)

#### 2. インスタンステンプレートを利用して、マネージドインスタンスグループを作成する
[マネージド インスタンス グループの作成](https://cloud.google.com/compute/docs/instance-groups/creating-groups-of-managed-instances?hl=ja)


#### 3. httpロードバランサーを設定する


#### 4. 負荷テストを実施して、インスタンスが自動スケーリングすることを確認する
* [インスタンスのグループの自動スケーリング](https://cloud.google.com/compute/docs/autoscaler?hl=ja)
* [負荷分散処理能力に基づくスケーリング](https://cloud.google.com/compute/docs/autoscaler/scaling-load-balancing?hl=ja)
