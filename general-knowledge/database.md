# Database

## MySQL

### 事务隔离级别 (隔离性依次增强，性能变差)

* read uncommitted: 事务可以读取其他事务尚未提交的数据。可能出现dirty read
* read committed: 只能读取已经提交的数据。避免脏读，可能出现unrepeatable read, e.g. 事务A首先读取了某个数据的值，事务B对该数据进行了修改并提交，事务A再次读取数据不一致，可能导致逻辑错误。
* repeatable read: 即使其他事务对数据进行了修改，先读取的事务也不会受到影响，它读取的仍然是最初创建的快照中的版本。通常针对数据UPDATE操作。可能出现幻读，因为对数据行的插入或删除操作，没有提供一致的快照。
* serializable: 事务之间没有并发。避免了脏读、不可重复读、幻读，但带来了性能损失。

### 主从复制

<figure><img src="../.gitbook/assets/db_master-slave.png" alt=""><figcaption></figcaption></figure>
