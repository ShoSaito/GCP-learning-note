# Google Kubernetes Engine クラスタをデプロイする

## ハンズオン
https://cloud.google.com/kubernetes-engine/docs/tutorials/hello-app?hl=ja


## 出来たこと



## これから調べること

- タグとは
- Pod @kubernetes
https://kubernetes.io/docs/concepts/workloads/pods/pod/
- gcloud config set compute/zoneは何をしているのか
- Container Registry とは
https://cloud.google.com/container-registry?hl=ja
- GCR
- WARNING 
WARNING: Currently VPC-native is not the default mode during cluster creation. In the future, this will become the default mode and can be disabled using `--no-enable-ip-alias` flag. Use `--[no-]enable-ip-alias` flag to suppress this warning.
WARNING: Newly created clusters and node-pools will have node auto-upgrade enabled by default. This can be disabled using the `--no-enable-autoupgrade` flag.
WARNING: Starting with version 1.18, clusters will have shielded GKE nodes by default.
WARNING: Your Pod address range (`--cluster-ipv4-cidr`) can accommodate at most 1008 node(s). 
This will enable the autorepair feature for nodes. Please see https://cloud.google.com/kubernetes-engine/docs/node-auto-repair for more information on node autorepairs.