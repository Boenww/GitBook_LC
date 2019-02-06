# 110. balanced binary tree

Given a binary tree, determine if it is height-balanced.

{% tabs %}
{% tab title="Notes" %}
Difference between up-bottom and bottom-up solutions.
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //up-bottom O(n^2)
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        
        return isBalanced(root.left) && isBalanced(root.right) &&
            Math.abs(getDepth(root.left) - getDepth(root.right)) <= 1;
    }
    
    public int getDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        return Math.max(getDepth(root.left), getDepth(root.right)) + 1;
    }
    
    //bottom-up O(n)
    public static final int NOT_BALANCED = -1; //or use ResultType class
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        
        return getDepth(root) != NOT_BALANCED;
    }
    
    public int getDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int left = getDepth(root.left);
        int right = getDepth(root.right);
        if (left == NOT_BALANCED || right == NOT_BALANCED || Math.abs(left - right) > 1) {
            return NOT_BALANCED;
        }
        
        return Math.max(left, right) + 1;
    }
}
```
{% endtab %}
{% endtabs %}



