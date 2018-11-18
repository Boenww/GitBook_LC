---
description: >-
  Given a undirected graph, a node and a target, return the nearest node to
  given node which value of it is target, return null if you can't find.
---

# search graph nodes

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /*
     * @param graph: a list of Undirected graph node
     * @param values: a hash mapping, <UndirectedGraphNode, (int)value>
     * @param node: an Undirected graph node
     * @param target: An integer
     * @return: a node
     */
    public UndirectedGraphNode searchNode(ArrayList<UndirectedGraphNode> graph,
                                          Map<UndirectedGraphNode, Integer> values,
                                          UndirectedGraphNode node,
                                          int target) {
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        Set<UndirectedGraphNode> visited = new HashSet<>();
        queue.offer(node);
        while (!queue.isEmpty()) {
            UndirectedGraphNode graphNode = queue.poll();
            if (values.get(graphNode) == target) {
                return graphNode;
            }
            visited.add(graphNode);
            for (UndirectedGraphNode nb: graphNode.neighbors) {
                if (!visited.contains(nb)) {
                    queue.offer(nb);
                }
            }
        }
        
        return null;
    }
}
```
{% endtab %}
{% endtabs %}

