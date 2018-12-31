# minimum subtree

Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.  


{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */
     
     //traverse + dc
    public TreeNode minNode = null;
    public int min = Integer.MAX_VALUE;
    
    public TreeNode findSubtree(TreeNode root) {
        getSum(root);
        
        return minNode;
    }
    
    public int getSum(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int left = getSum(root.left);
        int right = getSum(root.right);
        
        if (minNode == null || left + right + root.val <= min) {
            min = left + right + root.val;
            minNode = root;
        }
        
        return left + right + root.val;
    }
    
    //dc
    public TreeNode findSubtree(TreeNode root) {
        return helper(root).minNode;
    }
    
    public ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(root, 0, Integer.MAX_VALUE);
        }
        
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        ResultType res = new ResultType(root, root.val + left.sum + right.sum, root.val + left.sum + right.sum);
        
        if (left.minSum < res.minSum) {
            res.minSum = left.minSum;
            res.minNode = left.minNode;
        }
        
        if (right.minSum < res.minSum) {
            res.minSum = right.minSum;
            res.minNode = right.minNode;
        }
        
        return res;
    }
}

class ResultType {
    public TreeNode minNode;
    public int sum, minSum;
    public ResultType(TreeNode minNode, int sum, int minSum) {
        this.minNode = minNode;
        this.sum = sum;
        this.minSum = minSum;
    } 
}


```
{% endtab %}
{% endtabs %}

