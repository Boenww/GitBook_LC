# Queue

## add vs. offer

From the [`Queue`](http://java.sun.com/j2se/1.5.0/docs/api/java/util/Queue.html#offer\(E\)) interface

> When using queues that may impose insertion restrictions (for example capacity bounds), method `offer` is generally preferable to method `Collection.add(E)`, which can fail to insert an element only by throwing an exception.

`PriorityQueue` is a `Queue` implementation that does not impose any insertion restrictions. Therefore the `add` and `offer` methods have the same semantics.

## 实现方式

队列内部存储元素的方式，一般有两种，**数组**（array）和**链表**（linked list）。两者的最主要区别是：

* 数组对**随机访问**有较好性能。
* 链表对**插入**和**删除**元素有较好性能。

在各语言的标准库中：

* Java常用的队列包括如下几种：\
  `ArrayDeque`：数组存储。实现Deque接口，而Deque是Queue接口的子接口，代表**双端队列**（double-ended queue）。\
  `LinkedList`：链表存储。实现List接口和Duque接口，不仅可做队列，还可以作为双端队列，或栈（stack）来使用。
* C++中，使用\<queue>中的`queue`模板类，模板需两个参数，元素类型和容器类型，元素类型必要，而容器类型可选，默认`deque`，可改用`list`（链表）类型。
* Python中，使用`collections.deque`，双端队列。

## Applications

队列可用于实现消息队列（message queue），以完成异步（asynchronous）任务。

“消息”是计算机间传送的数据，可以只包含文本；也可复杂到包含嵌入对象。当消息“生产”和“消费”的速度不一致时，就需要消息队列，临时保存那些已经发送而并未接收的消息。例如集体打包调度，服务器繁忙时的任务处理，事件驱动等等。

常用的消息队列实现包括[RabbitMQ](http://www.rabbitmq.com/)，[ZeroMQ](http://zeromq.org/)等等。

更多消息队列的参考资料：\
[为什么需要消息队列，及使用消息队列的好处？](http://www.ywnds.com/?p=5791)\
[RabbitMQ的应用场景以及基本原理介绍](http://blog.csdn.net/whoamiyang/article/details/54954780)
