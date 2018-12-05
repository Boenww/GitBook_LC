# maximum depth of binary tree

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//recursive
public int maxDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }

    return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
}

//iterative
public int maxDepth(TreeNode root) {
    int depth = 0;

    if (root == null) {
        return depth;
    }

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while(!queue.isEmpty()) {
        int size = queue.size();

        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            if (node.left != null) {
                queue.offer(node.left);
            }

           if (node.right != null) {
               queue.offer(node.right);
           }
        }
        depth++;
    }

    return depth;
}
```
{% endtab %}
{% endtabs %}

