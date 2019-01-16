# Queue

## add vs. offer

From the [`Queue`](http://java.sun.com/j2se/1.5.0/docs/api/java/util/Queue.html#offer%28E%29) interface

> When using queues that may impose insertion restrictions \(for example capacity bounds\), method `offer` is generally preferable to method `Collection.add(E)`, which can fail to insert an element only by throwing an exception.

`PriorityQueue` is a `Queue` implementation that does not impose any insertion restrictions. Therefore the `add` and `offer` methods have the same semantics.

