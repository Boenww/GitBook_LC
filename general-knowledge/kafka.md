---
description: 分布式消息队列/distributed streaming platform
---

# Kafka

Producer, Consumer (Group), Broker (Kafka node server), Zookeeper

### Zookeeper

* 管理集群配置
* 选举leader
* consumer group变化时rebalance

<figure><img src="../.gitbook/assets/kafka components.png" alt=""><figcaption></figcaption></figure>

### Consumer group

每个consumer属于一个特定的consumer group，一条消息可发送多个consumer group，但一个consumer group中只能有一个consumer消费该消息。

### Partition

同一个topic的partition分别存储在kafka集群的多个broker上。存储层面讲，每个partition都是一个有序的、不可变的记录序列，通俗点就是一个append log文件。producer push的消息是append到partition中的，顺序写磁盘效率远高于随机写内存。

### Segment

实际的存储粒度，一个partition物理上由多个segment组成。由两部分组成，分别是.index索引和.log数据文件。索引文件中的元数据指向的是对应数据文件中消息的物理偏移地址。索引文件是有序的，可通过二分查找快速定位。如何判断读完一条消息？通过消息在磁盘上的物理存储结构（其中包含偏移量、消息体长度等可度量消息终止地址的数据）。

### Replica

<figure><img src="../.gitbook/assets/kafka replica.png" alt=""><figcaption></figcaption></figure>

* Leader: 跟producer和consumer交互；
* Follower: 被动备份leader中的数据
* ISR (In Sync Replica): 包含leader和所有与leader保持同步的follower
* OSR (Out of Sync Replica): 新加入的follower会先存放在OSR中

<figure><img src="../.gitbook/assets/HW &#x26; LEO.png" alt=""><figcaption></figcaption></figure>

HW (high watermark): HW <= LEO for a replica. msg <= HW 被认为是已备份的。每个replica负责更新自己的HW

LEO (log end offset): log最后一条msg的位置。

完全同步复制：受限于复制最慢的follower，极大影响吞吐率。异步复制：follower尚未完成复制的情况下，leader宕机，必然导致数据丢失。ISR策略是一种中庸且灵活的策略，has a tradeoff between reliability and throughput.&#x20;

