# trim a bst

Given a binary search tree and the lowest and highest boundaries as `L` and `R`, trim the tree so that all its elements lies in `[L, R]` \(R &gt;= L\). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

{% tabs %}
{% tab title="Notes" %}
* recursive: O\(n\), O\(n\)
* iterative: O\(n\), O\(1\)
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    public TreeNode trimBST(TreeNode root, int L, int R) {
        if (root == null) {
            return null;
        }
        
        if (root.val < L) {
            return trimBST(root.right, L, R);
        } 
        
        if (root.val > R) {
            return trimBST(root.left, L, R);
        }
        
        root.left = trimBST(root.left, L, R);
        root.right = trimBST(root.right, L, R);
        
        return root;
    }
    
    //iterative
    public TreeNode trimBST(TreeNode root, int L, int R) {
        if (root == null) {
            return null;
        }
        
        //1. find a valid root
        while (root != null && (root.val < L || root.val > R)) { // no node in L, R possibly
            if (root.val < L) {
                root = root.right;
            } else if (root.val > R) {
                root = root.left;
            }
        }
    
        //2. consider the left subtree
        TreeNode node = root;
        while (node != null) {
            while (node.left != null && node.left.val < L) {
                node.left = node.left.right;
            }
            node = node.left;
        }
        
        //3. consider the right subtree
        node = root;
        while (node != null) {
            while (node.right != null && node.right.val > R) {
                node.right = node.right.left;
            }
            node = node.right;
        }
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}

