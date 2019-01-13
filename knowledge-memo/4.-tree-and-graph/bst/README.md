# BST

## Features

* Inorder traversal -&gt; sorted in ascending order
* Average search O\(logn\)

## Red-black Tree

红黑树（Red-black Tree）是一种平衡排序二叉树（Balanced Binary Search Tree），在它上面进行增删查改的**平均**时间复杂度都是 O\(logn\).

Java当中，红黑树主要是`TreeSet`，位于`java.util.TreeSet`，继承自`java.util.AbstractSet`，它的主要方法有：

* `add`，插入一个元素。
* `remove`，删除一个元素。
* `clear`，删除所有元素。
* `contains`，查找是否包含某元素。
* `isEmpty`，是否空树。
* `size`，返回元素个数。
* `iterator`，返回迭代器。
* `clone`，对整棵树进行浅拷贝，即不拷贝元素本身。
* `first`，返回最前元素。
* `last`，返回最末元素。
* `floor`，返回不大于给定元素的最大元素。
* `ceiling`，返回不小于给定元素的最小元素。
* `pollFirst`，删除并返回首元素。
* `pollLast`，删除并返回末元素。

更具体的细节，请参考[Java Reference](https://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html)。

此外，在Java当中，有一种map，用红黑树实现key查找，这种结构叫做`TreeMap`。如果你需要一种map，并且它的key是有序的，那么强烈推荐`TreeMap`。

