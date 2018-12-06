# maximum depth of n-ary tree

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//recursive
public int maxDepth(Node root) {
    if (root == null) {
        return 0;
    }

    int max = 0;
    for (Node child: root.children) {
        max = Math.max(max, maxDepth(child));
    }

    return max + 1;
}

//iterative
public int maxDepth(Node root) {
    int depth = 0;
    if (root == null) {
        return depth;
    }

    Queue<Node> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        depth++;
        for (int i = 0; i < size; i++) {
            Node node = queue.poll();
            for (Node child: node.children) {
                queue.offer(child);
            }
        }
    }

    return depth;
}
```
{% endtab %}
{% endtabs %}

