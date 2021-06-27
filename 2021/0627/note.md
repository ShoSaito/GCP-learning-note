

## DB
### Cloud SQL
Cloud SQLはリレーショナルデータベースですが、マルチリージョン構成をサポートしていません。

### DataStore
* [クイックスタート](https://cloud.google.com/datastore/docs/quickstart)
* [復習：ACID特性](https://ja.wikipedia.org/wiki/ACID_(%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF%E7%A7%91%E5%AD%A6)) 

### BQ
BigQueryは複数ステートメントのトランザクションはサポートされていません。
BigQueryのアクティブストレージ料金は、Cloud Storage Nearlineストレージよりも高価です。

### Cloud Filestore 
[Cloud Filestore](https://cloud.google.com/filestore)は、データ用のファイルシステムインターフェースと共有ファイルシステムを必要とするアプリケーション向けのマネージドファイルストレージ サービスです。 Cloud Filestore ではファイルロックはサポートされます。

## GCS
[gsutil versioning set](https://cloud.google.com/storage/docs/gsutil/commands/versioning)


## GCE
### カスタム マシンタイプ
[カスタム マシンタイプの VM インスタンスを作成する](https://cloud.google.com/compute/docs/instances/creating-instance-with-custom-machine-type#gcloud)

N1 マシンタイプの場合は、gcloud compute instances create コマンドを使用して次のいずれかのオプションを指定します。
* --custom-cpu と --custom-memory フラグ。
* --machine-type=custom-[NUMBER_OF_CPUS]-[NUMBER_OF_MB] 

### OSログイン
[OSログイン](https://cloud.google.com/compute/docs/oslogin)を使用するとIAMの役割を使用してLinuxインスタンスへのSSHアクセスを管理できます。

### ヘルスチェック
[ヘルスチェックと自動修復の設定](https://cloud.google.com/compute/docs/instance-groups/autohealing-instances-in-migs)


## GAE
トラフィックを新しいバージョンに移行するには、gcloud app versions migrate [新しいバージョン] コマンドを実行します。


## GKE
Deploymentを使用してServiceを公開するには、kubectl expose deploymentコマンドで、--type、--port、--target-portパラメータを使用します。

[kubeconfig エントリの生成](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl#generate_kubeconfig_entry)



## Trace
[Stackdriver トレース](https://cloud.google.com/trace)はアプリケーション内でやり取りされるリクエストを追跡し、ほぼリアルタイムでパフォーマンスの分析情報を提供します。アプリケーションのトレースを自動的に分析し、パフォーマンス低下の原因となるレイテンシの詳細レポートを生成します。

## 予算アラート

[請求のロール](https://cloud.google.com/iam/docs/understanding-roles?hl=ja#billing-roles)
* Billing Account Administrator
* Billing Account User


## Cloud HSM
[概要](https://cloud.google.com/security-key-management)



## DM
[構成をプレビューする](https://cloud.google.com/deployment-manager/docs/configuration/preview-configuration-file)

* あまり触ったことがないので、この[チュートリアル](https://cloud.google.com/deployment-manager/docs/quickstart)をやっておく。
* [traformのチュートリアル](https://learn.hashicorp.com/collections/terraform/gcp-get-started)もやっておく。



## VPC
* [自動モード](https://cloud.google.com/vpc/docs/using-vpc?hl=ja-JPFactory)

* [カスタムルートのインポートとエクスポート](https://cloud.google.com/vpc/docs/vpc-peering#importing-exporting-routes)

* [ルートアドバタイズ](https://cloud.google.com/network-connectivity/docs/router/concepts/overview#route-advertisement)

* [Cloud VPN と Cloud Interconnect](https://cloud.google.com/network-connectivity/docs/how-to/choose-product?hl=ja)

VPCピアリングを利用すると、同じプロジェクトまたは組織に属しているかどうかに関わらず、２つの Virtual Private Cloud（VPC）ネットワーク間でプライベート RFC1918接続を確立できます。トラフィックはGoogleのネットワーク内に留まり、公共のインターネットを経由することはありません。

## Cloud Router
[Cloud Router](https://cloud.google.com/network-connectivity/docs/router) では、ボーダー ゲートウェイ プロトコル（BGP）を使用することで、Virtual Private Cloud（VPC）ネットワークとオンプレミス ネットワーク間でルートを動的に交換できます。例えば、オンプレミスサーバーとのVPNトンネルに使用する場合、Cloud RouterはVPC ネットワーク内の新しいサブネットを自動的に学習し、オンプレミス ネットワークに通知します。



