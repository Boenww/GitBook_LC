# search range in binary search tree

Given a binary search tree and a range `[k1, k2]`, return all elements in the given range.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public List<Integer> searchRange(TreeNode root, int k1, int k2) {
    List<Integer> res = new ArrayList<>();
    
    helper(root, res, k1, k2);
    return res;
}

public void helper(TreeNode root, List<Integer> res, int k1, int k2) {
    if (root == null) {
        return;
    }
    
    if (root.val > k2) {
        helper(root.left, res, k1, k2);
    } else if (root.val < k1) {
        helper(root.right, res, k1, k2);
    } else {
        helper(root.left, res, k1, k2);
        res.add(root.val);
        helper(root.right, res, k1, k2);
    }
}

//iterative
public List<Integer> searchRange(TreeNode root, int k1, int k2) {
    List<Integer> res = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();

    while (root != null) {
        if (root.val < k1) {
            root = root.right;
        } else {
            stack.push(root);
            root = root.left;
        }
    }

    while (!stack.isEmpty() && stack.peek().val <= k2) {
        TreeNode node = stack.pop();
        res.add(node.val);

        node = node.right;
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
    }

    return res;
}
```
{% endtab %}
{% endtabs %}

