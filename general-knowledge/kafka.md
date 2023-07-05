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
* Follower: 备份leader中的数据
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



**截断机制**：当宕机的旧leader重新上线时，会将自己的数据截断到宕机前HW位置，然后再同步新leader的数据。



消息生产过程中保证数据可靠性的策略（request.required.acks, min.insync.replicas）无法避免出现重复消息。例如producer发送消息给leader，leader同步数据给follower的时候宕机，此时选举出的新leader可能只有部分此次提交的数据，但生产者收到发送失败响应将重新发送数据。因此，kafka只支持at most once & at least once, not exactly once。消息去重需要在具体业务中实现，做好幂等，数据库方面可以（唯一键和主键）避免重复。



Kafka java 客户端使用异步方式发送消息，实际上将消息放入了一个后台发送队列，之后由一个后台线程不断地从队列中取出消息并发送。

**linger.ms**: 如果消息到达的速度比后台线程发送到partition的速度快，则会出现消息堆积的问题。这时客户端可通过添加人工延迟来减少请求数量，也就是说，producer将等待给定延迟后才允许发送其它消息。其具有减少发送请求数量的效果，但在没有负载的情况下将增加延迟。

**buffer.memory**: 消息堆积策略参数，producer可以用来缓冲等待发送给服务器消息的字节数。

**max.block.ms**: 消息堆积策略参数，在buffer.memory被占满后，producer可阻塞的最大时间，之后将抛出异常。

**批量发送**：当消息的目标partition相同时，producer会尝试batch request。

可通过参数max.in.flight.requests.per.connection = 1避免消息重排序问题（T1, T2 -> T1 fails and T2 succeeds, T1 retries -> T2, T1）



**活锁**：消费者持续维持心跳，但没有进行消息处理。利用max.poll.interval.ms活跃检测机制。



