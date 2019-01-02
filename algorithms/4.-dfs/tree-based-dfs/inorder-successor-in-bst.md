# inorder successor in bst

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

If the given node has no in-order successor in the tree, return `null`.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null || p == null) {
            return null;
        }
        
        if (root.val > p.val) {
            TreeNode node = inorderSuccessor(root.left, p);
            return node == null ? root : node;
        } else {
            return inorderSuccessor(root.right, p);
        }
    }
    
    //iterative
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        
        while (root != null) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }
        
        return successor;
    }
}
```
{% endtab %}
{% endtabs %}

