---
description: Find the number connected component in the undirected graph.
---

# connected component in undirected graph

{% tabs %}
{% tab title="Notes" %}
* BFS
* Union find
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /*
     * @param nodes: a array of Undirected graph node
     * @return: a connected set of a Undirected graph
     */
    public List<List<Integer>> connectedSet(List<UndirectedGraphNode> nodes) {
        List<List<Integer>> res = new ArrayList<>();
        Set<UndirectedGraphNode> visited = new HashSet<>();
        
        for (UndirectedGraphNode node: nodes) {
            if (visited.contains(node)) {
                continue;
            }
            
            List<Integer> connected = new ArrayList<>();
            Queue<UndirectedGraphNode> queue = new LinkedList<>();
            queue.offer(node);
            visited.add(node);
            connected.add(node.label);
            
            while (!queue.isEmpty()) {
                UndirectedGraphNode n = queue.poll();
                for (UndirectedGraphNode nb: n.neighbors) {
                    if (visited.contains(nb)) {
                        continue;
                    }
                    queue.offer(nb);
                    visited.add(nb);
                    connected.add(nb.label);
                }
            }
            Collections.sort(connected);
            res.add(connected);
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

