# When to use BFS

* Level Order Traversal
* Connected Component 由点及面
* Topological Sorting
* Shortest Path in Simple Graph\(equal edge length\)

## BFS in binary tree vs. in graph

二叉树中进行 BFS 和图中进行 BFS 最大的区别就是二叉树中无需使用 HashSet（C++: unordered\_map, Python: dict\) 来存储访问过的节点（丢进过 queue 里的节点）。因为二叉树这种数据结构，上下层关系分明，没有环（circle），所以不可能出现一个节点的儿子的儿子是自己的情况。但是在图中，一个节点的邻居的邻居就可能是自己了。

## 什么时候需要分层遍历

1. 如果问题需要区分开不同层级的结果信息，如 Binary Tree Level Order Traversal
2. 简单图最短路径问题，如 单词接龙 Word Ladder

## bidirectional bfs

#### 算法描述

双向宽度优先搜索本质上还是BFS，只不过变成了起点向终点和终点向起点同时进行扩展，直至两个方向上出现同一个子节点，搜索结束。我们还是可以利用队列来实现：一个队列保存从起点开始搜索的状态，另一个保存从终点开始的状态，两边如果相交了，那么搜索结束。起点到终点的最短距离即为起点到相交节点的距离与终点到相交节点的距离之和。

**Q.双向BFS是否真的能提高效率？**  
假设单向BFS需要搜索 N 层才能到达终点，每层的判断量为 X，那么总的运算量为 X ^ N. 如果换成是双向BFS，前后各自需要搜索 N / 2 层，总运算量为 2 \* X ^ {N / 2}。如果 N 比较大且X 不为 1，则运算量相较于单向BFS可以大大减少，差不多可以减少到原来规模的根号的量级。

