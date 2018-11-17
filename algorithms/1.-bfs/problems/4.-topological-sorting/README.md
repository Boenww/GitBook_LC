---
description: 拓扑排序是对有向无环图(dag)的顶点的一种排序，它使得如果存在一条从顶点A到顶点B的路径，那么在排序中B出现在A的后面且每个顶点出现且只出现一次。
---

# 4. Topological Sorting

## Concepts

* In-degree and out-degree
* It's not traditional sorting algorithm; one graph could have multiple topological orders and also could have no one topological order

## Algorithm

1. 统计每个点的入度，并初始化拓扑序列为空
2. 将所有入度为 0 的点放到宽搜的队列中
3. 将宽搜队列中的点一个一个的释放出来，放到拓扑序列中，每次释放出某个点的时候，就访问所有它指向的点并把这些点的入度减1
4. 如果发现某个点的入度被减去1之后变成0，则放入宽搜队列中。
5. 算法执行到宽搜队列为空时

## Practical Application

* 检测编译时的循环依赖
* 制定有依赖关系的任务的执行顺序

