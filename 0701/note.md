# リソースへのアクセス権の付与、変更、取り消し

## 公式doc
https://cloud.google.com/iam/docs/granting-changing-revoking-access

### 基本のロールについて


## ノート
### 基本ロール
* 基本ロール: Cloud IAM の導入前に存在していたオーナー、編集者、閲覧者のロールが含まれます。
* 事前定義ロール: 特定のサービスへのアクセスを細かく制御します。また、Google Cloud により管理されます。
* カスタムロール: ユーザー指定の権限のリストに応じたきめ細かなアクセス権が提供されます。

https://cloud.google.com/iam/docs/understanding-roles

### 権限の付与@コンソール
コンソール上では主に2つのレベルで管理可能になっている。
1. プロジェクトレベル
表示しているプロジェクトのレベルでユーザーの追加が可能
![](2020-07-07-09-14-45.png)

2. 組織レベル
プロジェクトから一つ階層をあげたレベルでも管理が可能
![](2020-07-07-09-57-43.png)


### gcloudを利用した権限の付与

構文
```
gcloud group add-iam-policy-binding resource \
    --member=member --role=role-id
```

例
```
gcloud projects add-iam-policy-binding my-project \
    --member=user:my-user@example.com --role=roles/viewer
```
#### `gcloud project`コマンド
権限の付与は`gcloud project`で行う。
`gcloud project`はプロジェクトの管理を行うコマンドが含まれている。

[`gcloud project`](https://cloud.google.com/sdk/gcloud/reference/projects/)

### 権限が持てるモノ
#### どんなモノに権限付与できる❓

> member に使用できる値の一覧については、[ポリシー バインディングのリファレンス](https://cloud.google.com/iam/docs/reference/rest/v1/Policy#Binding)をご覧ください。

リンク先を確認すると、下記の様なモノに権限が付与できることが確認できる。
* user
* service account
* group
* domain
* 削除したuserとかもある。この辺りのどんなユースケースが想定されているのだろう
* allUsersとかもある。誰でも編集できるGCPプロジェクトを作成できるってこと⁇

#### どんなユーザー(ドメイン)でも権限付与可能なのか❓
G Suiteドメインか、Cloud Identityで設定したものでないとNG

> 注: メンバータイプ user の場合、識別子に含まれるドメイン名は G Suite ドメインまたは Cloud Identity ドメインである必要があります。Cloud Identity ドメインの設定方法については、Cloud Identity の概要をご覧ください


##### [Cloud Identity](https://cloud.google.com/identity/docs/overview)とは
リンク先を読んでみるとIDaaSだと言うことは分かった。
(Azure) Active Directoryとかと連携できる。

[日本語の説明](https://support.google.com/cloudidentity/answer/7319251?hl=ja)

> 有料の G Suite アカウントとは別に、各ユーザーに無料の Cloud Identity アカウントを作成することで、ドメイン内のすべてのユーザーを Google 管理コンソールから管理できます。

下記から設定可能
![](2020-07-21-09-23-38.png)

### プログラムによる権限の付与


## 要点まとめ

### 権限範囲・権限内容(where、what)
* GCPには基本のロールがある。広範なリソースに対して、権限が事前定義されている。
* まずは基本ロールの利用を検討し、ユースケースによって適用範囲を個別に指定できる。
* 権限内容は独自にカスタマイズできる。

### 権限管理方法(how)
* 権限の付与方法は3つある。
    * GCPコンソール
    * gcloud これは`gcloud project`で行う。


## 宿題