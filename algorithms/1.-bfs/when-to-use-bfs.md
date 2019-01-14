# When to use BFS & b-bfs

* Level Order Traversal
* Connected Component 由点及面
* Topological Sorting
* Shortest Path in Simple Graph\(equal edge length\)

## bidirectional bfs

#### 算法描述

双向宽度优先搜索本质上还是BFS，只不过变成了起点向终点和终点向起点同时进行扩展，直至两个方向上出现同一个子节点，搜索结束。我们还是可以利用队列来实现：一个队列保存从起点开始搜索的状态，另一个保存从终点开始的状态，两边如果相交了，那么搜索结束。起点到终点的最短距离即为起点到相交节点的距离与终点到相交节点的距离之和。

**Q.双向BFS是否真的能提高效率？**  
假设单向BFS需要搜索 N 层才能到达终点，每层的判断量为 X，那么总的运算量为 X ^ N. 如果换成是双向BFS，前后各自需要搜索 N / 2 层，总运算量为 2 \* X ^ {N / 2}。如果 N 比较大且X 不为 1，则运算量相较于单向BFS可以大大减少，差不多可以减少到原来规模的根号的量级。

