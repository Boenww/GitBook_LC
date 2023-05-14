# 110. balanced binary tree

Given a binary tree, determine if it is height-balanced.

{% tabs %}
{% tab title="Notes" %}
Difference between up-bottom and bottom-up solutions.

up-bottom:

首先需要遍历树中所有节点，i.e. O(n). 对于某一节点，如果它的高度是h, 则getDepth最多会被调用h次，最坏情况下二叉树为链式结构，高度为O(n)，此时总时间复杂度为O(n^2).

bottom-up:

每个节点的计算高度和判断是否平衡都只需要处理一次，因此O(n).
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





