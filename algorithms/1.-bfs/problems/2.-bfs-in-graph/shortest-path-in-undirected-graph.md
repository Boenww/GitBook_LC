# shortest path in undirected graph

Give an `undirected graph`, in which each edge's length is `1`, and give `two` nodes from the graph. We need to find the `length` of `the shortest path` between the given `two` nodes.

{% tabs %}
{% tab title="Notes" %}
* Bidirectional bfs 
* pay attention to level information!!!
{% endtab %}

{% tab title="Solution" %}
```java
/**
 * Definition for graph node.
 * class GraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public class Solution {
    /**
     * @param graph: a list of Undirected graph node
     * @param A: nodeA
     * @param B: nodeB
     * @return:  the length of the shortest path
     */
    public int shortestPath(List<UndirectedGraphNode> graph, UndirectedGraphNode A, UndirectedGraphNode B) {
        int shortest = 0;
        if (A == B) {
            return shortest;
        }
        
        Queue<UndirectedGraphNode> startQueue = new LinkedList<>();
        Set<UndirectedGraphNode> startVisited = new HashSet<>();
        startQueue.offer(A);
        startVisited.add(A);
        Queue<UndirectedGraphNode> endQueue = new LinkedList<>();
        Set<UndirectedGraphNode> endVisited = new HashSet<>();
        endQueue.offer(B);
        endVisited.add(B);
        while (!startQueue.isEmpty() && !endQueue.isEmpty()) {
            shortest++;
            int startSize = startQueue.size();
            for (int i = 0; i < startSize; i++) {
                UndirectedGraphNode startNode = startQueue.poll();
                for (UndirectedGraphNode nb: startNode.neighbors) {
                    if (startVisited.contains(nb)) {
                        continue;
                    }
                
                    if (endVisited.contains(nb)) {
                        return shortest;
                    }
                
                    startVisited.add(nb);
                    startQueue.offer(nb);
                }
            }
            
            shortest++;
            int endSize = endQueue.size();
            for (int j = 0; j < endSize; j++) {
                UndirectedGraphNode endNode = endQueue.poll();
                for (UndirectedGraphNode nb: endNode.neighbors) {
                    if (endVisited.contains(nb)) {
                        continue;
                    }
                
                    if (startVisited.contains(nb)) {
                        return shortest;
                    }
                
                    endVisited.add(nb);
                    endQueue.offer(nb);
                }
            }
        }
        
        return -1;
    }
}
```
{% endtab %}
{% endtabs %}

