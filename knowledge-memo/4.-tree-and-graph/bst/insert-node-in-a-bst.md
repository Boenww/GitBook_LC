# insert node in a bst

Given a binary search tree and a new tree node, insert the node into the tree. You should keep the tree still be a valid binary search tree.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        
        if (root.val > val) {
            root.left = insertIntoBST(root.left, val);
        } else {
            root.right = insertIntoBST(root.right, val);
        }
        
        return root;
    }
    
    //iterative
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        
        TreeNode cur = root, lastNode = null;
        while (cur != null) {
            lastNode = cur;
            cur = cur.val > val ? cur.left : cur.right;
        }
        
        if (lastNode.val > val) {
            lastNode.left = new TreeNode(val);
        } else {
            lastNode.right = new TreeNode(val);
        }
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}

