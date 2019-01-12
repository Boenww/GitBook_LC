# 1. Hash Table

![](../../.gitbook/assets/1861542479286_.pic_hd%20%281%29.jpg)

## Get && Set

O\(size of key\)

## Open Hashing

是指哈希表所基于的数组中，每个位置是一个 Linked List 的头结点。这样冲突的 &lt;key, value&gt; 二元组，就都放在同一个链表中。

## Close Hashing 

是指在发生冲突的时候，后来的元素，往下一个位置去找空位。

![](../../.gitbook/assets/1871542479518_.pic_hd%20%281%29.jpg)

## Collision

Chaining with LinkedLists: In the worst case, lookup is 0 \(n\), where n is the number of elements in the hash table. This would only happen with either some very strange data or a very poor hash function \(or both\).

Chaining with BSTs: worst-case run time O\(logn\), but rarely tooken in practice because of nonuniform distribution.

Open Addressing with Linear Probing\(close hashing\): limited by the size of the array; cluster

Quadratic Probing and Double Hashing

