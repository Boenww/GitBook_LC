# binary tree zigzag order traversal

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) {
        return res;
    }

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    boolean leftToRight = true;
    while (!queue.isEmpty()) {
        List<Integer> level = new ArrayList<>();
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            if (leftToRight) {
                level.add(node.val);
            } else {
                level.add(0, node.val);
            }

            if (node.left != null) {
                queue.offer(node.left);
            }

            if (node.right != null) {
                queue.offer(node.right);
            }
        }

        res.add(level);
        leftToRight = !leftToRight;
    }

    return res;
}
```
{% endtab %}
{% endtabs %}

