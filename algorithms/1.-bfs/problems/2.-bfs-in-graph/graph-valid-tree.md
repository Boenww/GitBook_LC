---
description: >-
  Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each
  edge is a pair of nodes), write a function to check whether these edges make
  up a valid tree.
---

# graph valid tree

{% tabs %}
{% tab title="Notes" %}
Two conditions to judge if it is a valid tree

1. If it is acyclic -&gt; relationship between \# of edges and \# of nodes
2. If it is connected\(there can be two trees which is not a valid tree\): can bfs all nodes?
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        //condition 1 no cycle: # of edges = # of nodes - 1
        if (edges.length != n - 1) {
            return false;
        }
        
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<>());
        }
        
        for (int i = 0; i < edges.length; i++) {
            graph.get(edges[i][0]).add(edges[i][1]);
            graph.get(edges[i][1]).add(edges[i][0]);
        }
        
        boolean[] visited = new boolean[n];
        int count = 0;
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(0);
        while (!queue.isEmpty()) {
            Integer node = queue.poll();
            visited[node] = true;
            count++;
            for (Integer nb: graph.get(node)) {
                if (!visited[nb]) {
                    queue.offer(nb);
                }
            }
        }
        
        //condition 2 connected: bfs all nodes?
        return count == n;
    }
}
```
{% endtab %}
{% endtabs %}

