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
```
{% endtab %}
{% endtabs %}

