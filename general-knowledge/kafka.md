---
description: 分布式消息队列/distributed streaming platform
---

# Kafka

Producer, Consumer (Group), Broker (Kafka node server), Zookeeper

<figure><img src="../.gitbook/assets/kafka components.png" alt="producer must specify the topic when pushing msgs"><figcaption></figcaption></figure>

### Zookeeper

* 管理集群配置（broker, topic, producer, consumer注册（实质为文件目录），topic与broker的关系，consumer与partition的关系）
* 负载均衡
* 选举leader
* consumer group变化时rebalance

### Consumer group

每个consumer属于一个特定的consumer group，一条消息可发送多个consumer group，但一个consumer group中只能有一个consumer消费该消息。

### Partition

同一个topic的partition分别存储在kafka集群的多个broker上。存储层面讲，每个partition都是一个有序的、不可变的记录序列，通俗点就是一个append log文件。producer push的消息是append到partition中的，顺序写磁盘效率远高于随机写内存。e.g. 4 partitions of topic "mytopic\_test" in kafka log directory

```
drwxr-xr-x 2 root root 4096 Oct 15 13:21 mytopic_test-0
drwxr-xr-x 2 root root 4096 Oct 15 13:21 mytopic_test-1
drwxr-xr-x 2 root root 4096 Oct 15 13:21 mytopic_test-2
drwxr-xr-x 2 root root 4096 Oct 15 13:21 mytopic_test-3
```

### Segment

实际的存储粒度，一个partition物理上由多个segment组成。由两部分组成，分别是.index索引和.log数据文件。索引文件中的元数据指向的是对应数据文件中消息的物理偏移地址。索引文件是有序的，可通过二分查找快速定位。如何判断读完一条消息？通过消息在磁盘上的物理存储结构（其中包含偏移量、消息体长度等可度量消息终止地址的数据）。e.g. in mytopic\_test-0 folder

```
00000000000000000000.index
00000000000000000000.log
00000000000000170410.index
00000000000000170410.log
00000000000000239430.index
00000000000000239430.log
```

### Replica

<figure><img src="../.gitbook/assets/kafka replica.png" alt=""><figcaption></figcaption></figure>

* Leader: 跟producer和consumer交互；
* Follower: 被动备份leader中的数据
* ISR (In Sync Replica): 包含leader和所有与leader保持同步的follower，动态变化的
* OSR (Out of Sync Replica): 当follower从leader同步数据延迟超过阈值（replica.lag.time.max.ms）时，将被剔除出ISR，存入OSR。

<figure><img src="../.gitbook/assets/HW &#x26; LEO.png" alt=""><figcaption></figcaption></figure>

HW (high watermark): HW <= LEO for a replica. msg <= HW 被认为是已备份的。每个replica负责更新自己的HW

LEO (log end offset): log最后一条msg的位置。

完全同步复制：受限于复制最慢的follower，极大影响吞吐率。异步复制：follower尚未完成复制的情况下，leader宕机，必然导致数据丢失。ISR策略是一种中庸且灵活的策略，has a tradeoff between reliability and throughput.&#x20;



**如何保证可靠性的前提下避免吞吐量下降？**

request.required.acks=-1, min.insync.replicas



### 负载均衡

* Producer: 将消息均衡地push到各个partition。低级接口中可以指定partition，但对负载均衡不友好。高级接口中一般不支持partition接口，隐藏了内部轮询、对传入key进行hash等策略从而均衡发送到各个partition的细节。
* Consumer: 均衡地消费消息。基于zookeeper提供的watcher，consumer可以监听同一group中consumer的变化，以及broker的变化，进而根据consumer列表，将partition排序后，轮流分配。这一负载均衡的动态过程叫rebalance。





