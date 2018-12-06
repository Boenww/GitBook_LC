---
description: 'Given a binary tree, find its minimum depth.'
---

# minimum depth of binary tree

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//recursive
public int minDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }

    return getMin(root);
}

public int getMin(TreeNode node) {
    if (node == null) {
        return Integer.MAX_VALUE; //make no effect on the other branch
    }

    if (node.left == null && node.right == null) {
        return 1;
    }

    return Math.min(getMin(node.left), getMin(node.right)) + 1;
}

//iterative
public int minDepth(TreeNode root) {
    int depth = 0;
    if (root == null) {
        return depth;
    }

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        depth++;
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            if (node.left == null && node.right == null) {
                return depth;
            } 

            if (node.left != null) {
                queue.offer(node.left);
            }

            if (node.right != null) {
                queue.offer(node.right);
            }
        }
    }

    return depth;
}
```
{% endtab %}
{% endtabs %}

