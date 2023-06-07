# Docker & k8s

## Docker



## k8s

<figure><img src="../.gitbook/assets/k8s.jpeg" alt=""><figcaption><p>架构组成</p></figcaption></figure>

* master主节点：expose api，调度部署和节点管理
  * etcd: 保存所有集群数据的数据库
  * apiserver: expose api, the bridge between the client and k8s cluster
  * controller-manager: 负责维护群集的状态，比如故障检测、自动扩展、滚动更新等
  * scheduler: 让pod在合适的节点上创建运行，资源调度
* 计算节点：真正工作的节点
  * pod: smallest unit in k8s and can run multiple containers（豌豆夹和豌豆）
  * kubelet: node的代理，维护容器的生命周期
  * kube-proxy: node的网络代理，负责为service提供负载均衡将请求转发到pod上



### 创建pod过程

1. client -pod配置-> apiserver
2. apiserver -> controller mgr
3. controller mgr -> apiserver -> pod配置 -> etcd
4. scheduler -> 选择适合pod资源配置要求的节点 -pod资源配置单-> node的kubelet
5. kubelet -pod运行信息-> scheduler -> etcd

### 删除pod过程



