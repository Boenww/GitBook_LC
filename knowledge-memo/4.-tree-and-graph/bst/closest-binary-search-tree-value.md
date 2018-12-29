# closest binary search tree value

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

* Given target value is a floating point.
* You are guaranteed to have only one unique value in the BST that is closest to the target.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return 0;
        }
        
        if (root.val < target) {
            int right = closestValue(root.right, target);
            if (root.right != null && Math.abs(root.val - target) > Math.abs(right - target)) {
                return right;
            }
        } else {
            int left = closestValue(root.left, target);
            if (root.left != null && Math.abs(root.val - target) > Math.abs(left - target)) {
                return left;
            } 
        }
        
        return root.val;
    }
    
    //iterative
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return 0;
        }
        
        int res = root.val;
        
        while (root != null) {
            if (Math.abs(root.val - target) < Math.abs(res - target)) {
                res = root.val;
            }
            
            root = root.val > target ? root.left : root.right;
        }
        
        return res;
    } 
}
```
{% endtab %}
{% endtabs %}

