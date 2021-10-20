
# Kubernetesでアプリケーションを作成
2021/04/29


[Redis と PHP を使用したゲストブックの作成](https://cloud.google.com/kubernetes-engine/docs/tutorials/guestbook)をやってみた


#### gcloudの状態を確認する
```
gcloud config list
```
作業環境の確認を行う。

#### Kubernetesクラスタの作成
```
gcloud container clusters create guestbook --num-nodes=4

kubeconfig entry generated for guestbook.
NAME       LOCATION           MASTER_VERSION    MASTER_IP      MACHINE_TYPE  NODE_VERSION      NUM_NODES  STATUS
guestbook  [MY_ZONE]  1.18.16-gke.2100  [EX_IP]  e2-medium     1.18.16-gke.2100  4          RUNNING
```

結果の確認
```
gcloud container clusters listg
gcloud container clusters describe guestbook
```
#### アプリケーションのソースコードを用意
```
git clone https://github.com/GoogleCloudPlatform/kubernetes-engine-samples
cd kubernetes-engine-samples/guestbook
git checkout abbb383
```

#### Kubernetesにアプリケーションのデプロイ
現在のコンテクストの確認(操作したい環境のものか事前に確認。事故防止)
```
Kubectl config current-context

gke_[MY_GCPENV]_[MY_ZONE]_guestbook
```

デプロイ
```
kubectl apply -f redis-leader-deployment.yaml
kubectl get pods
```

redis-leader-deployment.yamlの中身
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-leader
  labels:
    app: redis
    role: leader
    tier: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
        role: leader
        tier: backend
    spec:
      containers:
      - name: leader
        image: "docker.io/redis:6.0.5"
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 6379
```
yamlの書き方



デプロイメントのログ確認、`Ready to accept connections`が確認できればOKらしい。
```
kubectl logs deployment/redis-leader

1:C [DATE TIME] # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C [DATE TIME] # Redis version=6.0.5, bits=64, commit=00000000, modified=0, pid=1, just started
1:C [DATE TIME] # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M [DATE TIME] * Running mode=standalone, port=6379.
1:M [DATE TIME] # Server initialized
1:M [DATE TIME] # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
1:M 08 May 2021 06:31:48.281 * Ready to accept connections
```



