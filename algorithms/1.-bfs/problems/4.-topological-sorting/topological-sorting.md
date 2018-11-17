# topological sorting

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

		Map<DirectedGraphNode, Integer> map = new HashMap<>();

		for (DirectedGraphNode node: graph) {
			for (DirectedGraphNode nb: node.neighbors) {
				if (map.containsKey(nb)) {
					map.put(nb, map.get(nb) + 1);
				} else {
					map.put(nb, 1);
				}
			}
		}

		Queue<DirectedGraphNode> queue = new LinkedList<>();
		for (DirectedGraphNode node: graph) {
			if (!map.containsKey(node)) {
				queue.offer(node);
			}
		}

		while (!queue.isEmpty()) {
			DirectedGraphNode node = queue.poll();
			res.add(node);
			for (DirectedGraphNode nb: node.neighbors) {
				if (map.get(nb) - 1 == 0) {
					queue.offer(nb);
				}
				map.put(nb, map.get(nb) - 1);
			}
		}

		return res;
	}
}
```
{% endtab %}
{% endtabs %}



