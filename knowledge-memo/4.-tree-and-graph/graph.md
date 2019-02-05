# Graph

### connected graph

 there is a path between every pair of vertices

## 如何定义

### adjacency list

an array of list to represent 

### adjacency matrix

less efficient, need to iterate through all the nodes to identify a node's neighbors

## 面试选择

### **1. 自定义邻接表**

```java
class DirectedGraphNode {
    int label;
    List<DirectedGraphNode> neighbors;
    ...
}
```

### 2. 使用 HashMap 和 HashSet 搭配的方式来存储邻接表

```java
Map<T, Set<T>> = new HashMap<Integer, HashSet<Integer>>();
```

