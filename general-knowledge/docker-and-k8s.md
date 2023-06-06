# Docker & k8s

## Docker



## k8s

架构组成

* master主节点：expose api，调度部署和节点管理
  * etcd: 保存所有集群数据的数据库
  * apiserver: expose api, the bridge between the client and k8s cluster
  * controller-manager: 负责维护群集的状态，比如故障检测、自动扩展、滚动更新等
  * scheduler: 让pod在合适的节点上创建运行，资源调度
* 计算节点：真正工作的节点
  * pod: smallest unit in k8s and can run multiple containers（豌豆夹和豌豆）
  * kubelet: node的代理，维护容器的生命周期
  * kube-proxy: node的网络代理，负责为service提供负载均衡将请求转发到pod上

