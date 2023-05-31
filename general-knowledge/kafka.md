---
description: 分布式消息队列/distributed streaming platform
---

# Kafka

## Zookeeper

* 管理集群配置
* 选举leader
* consumer group变化时rebalance

<figure><img src="../.gitbook/assets/kafka components.png" alt=""><figcaption></figcaption></figure>

Consumer group

每个consumer属于一个特定的consumer group，一条消息可发送多个consumer group，但一个consumer group中只能有一个consumer消费该消息。
