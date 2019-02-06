---
description: lintcode
---

# 127. topological sorting

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class DirectedGraphNode {
	public int label;
	public ArrayList<DirectedGraphNode> neighbors;
	public DirectedGraphNode(int label) {
		this.label = label;
		neighbors = new ArrayList<>();
	}
}

public class Solution {
	public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
		ArrayList<DirectedGraphNode> res = new ArrayList<>();
		if (graph == null || graph.size() == 0) {
			return res;
		}
		
		//1. stat indegree
		Map<DirectedGraphNode, Integer> map = getIndegree(graph);
		Queue<DirectedGraphNode> queue = new LinkedList<>();
		for (DirectedGraphNode node: graph) {
			if (!map.containsKey(node)) {
				queue.offer(node);
			}
		}
		
		//2. bfs
		while (!queue.isEmpty()) {
			DirectedGraphNode node = queue.poll();
			res.add(node);
			for (DirectedGraphNode nb: node.neighbors) {
				if (map.get(nb) == 1) {
					queue.offer(nb);
				}
				
				map.put(nb, map.get(nb) - 1);
			}
		}

		return res;
	}
	
	private Map<DirectedGraphNode, Integer> getIndegree(ArrayList<DirectedGraphNode> graph) {
		Map<DirectedGraphNode, Integer> res = new HashMap<>();
        for (DirectedGraphNode node: graph) {
            for (DirectedGraphNode nb: node.neighbors) {
                if (!res.containsKey(nb)) {
                    res.put(nb, 0);
                }
            
                res.put(nb, res.get(nb) + 1);
            }
        }

        return res;
	}
}
```
{% endtab %}
{% endtabs %}



