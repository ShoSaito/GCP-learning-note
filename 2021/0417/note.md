

### gcloud subnet cmd
* [公式doc](https://cloud.google.com/sdk/gcloud/reference/compute/networks/subnets) 

```bash
gcloud compute networks subnets COMMAND [GCLOUD_WIDE_FLAG …]
```

下記の操作のコマンド
Compute Engine subnetworks
VPC subnetworks.

### VPCとは

* [公式doc](https://cloud.google.com/vpc/docs/vpc)
共有VPC
CloudVPN
CloudInternconnect
VPCピアリング

### gcloud フィルタの使い方
* [公式doc](https://cloud.google.com/sdk/gcloud/reference/topic/filters?hl=ja)
* [公式blog](https://cloudplatform-jp.googleblog.com/2016/06/gcloud.html)

### インスタンス
```bash
gcloud compute instances list
```

### インスタンステンプレート
```bash
gcloud compute instace-template create \    
    --machine-type e2-standard-4 \
    --image-family debian-10 \
    --image-project debian-cloud \
    --boot-disk-size 250GB
```

OSの種類, マシンタイプ, などを指定できる。
dockerのイメージから、Dockerfileを生成出来たり、その逆のが出来るのと同じイメージ。


### イメージ
```bash
gcloud beta compute images describe-from-family IMAGE_FAMILY_NAME  \
   --project=IMAGE_PROJECT \
   --zone=ZONE
```

### マシンタイプ
スペックの高い順番に
```
1. A2
2. C2,
3. M1, M2
4. N2, N2D, N1
5. E2
```

#### マシンイメージ、永続ディスクのスナップショット、インスタンス テンプレート、カスタム イメージ比較

* [公式doc表](https://cloud.google.com/compute/docs/machine-images?hl=ja)

マシンイメージが一番汎用的、だけど高い
