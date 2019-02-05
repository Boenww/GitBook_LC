# 133. clone graph

Given the head of a graph, return a deep copy \(clone\) of the graph. Each node in the graph contains a `label` \(`int`\) and a list \(`List[UndirectedGraphNode]`\) of its `neighbors`. There is an edge between the given node and each of the nodes in its neighbors.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */

public class Solution {
    /*
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) {
            return null;
        }
        
        //1. find and copy all nodes
        List<UndirectedGraphNode> nodes = getNodes(node); 
        Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<>();
        for (UndirectedGraphNode n: nodes) {
            map.put(n, new UndirectedGraphNode(n.label));
        }
        
        //2. copy all edges
        for (UndirectedGraphNode n: nodes) {
            UndirectedGraphNode newNode = map.get(n);
            for (UndirectedGraphNode nb: n.neighbors) {
                newNode.neighbors.add(map.get(nb));
            }
        }
        
        return map.get(node);
    }
    
    private List<UndirectedGraphNode> getNodes(UndirectedGraphNode node) {
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        Set<UndirectedGraphNode> set = new HashSet<>();
        queue.offer(node);
    
        while (!queue.isEmpty()) {
            UndirectedGraphNode graphNode = queue.poll();
            set.add(graphNode);
            for (UndirectedGraphNode nb: graphNode.neighbors) {
                if (set.contains(nb)) {
                    continue;    
                }
                
                set.add(nb);
                queue.offer(nb);
            }
        }
        
        return new ArrayList<>(set);
    } 
}
```
{% endtab %}
{% endtabs %}

