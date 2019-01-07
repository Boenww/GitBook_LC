# closest binary search tree value I && II

## I

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

## II

Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

**Note:**

* Given target value is a floating point.
* You may assume k is always valid, that is: k ≤ total nodes.
* You are guaranteed to have only one unique set of k values in the BST that are closest to the target.

{% tabs %}
{% tab title="Notes" %}
* O\(n\): straightforward -&gt; but can use linked list for simplicity
* O\(klogn\): use two stacks
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //O(n) with LinkedList
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> res = new LinkedList<>();
        if (root == null || k == 0) {
            return res;
        }
        
        helper(root, target, k, res);
        return res;
    }
    
    public void helper(TreeNode root, double target, int k, List<Integer> res) {
        if (root == null) {
            return;
        }
        
        helper(root.left, target, k, res);
        
        if (res.size() < k) {
            res.add(root.val);
        } else {
            if (Math.abs(root.val - target) < Math.abs(res.get(0) - target)) {
                res.remove(0);
                res.add(root.val);
            }
        }
        
        helper(root.right, target, k, res);
    }
    
    //O(klogn)
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> res = new ArrayList<>();
        if (root == null || k == 0) {
            return res;
        }
        
        Stack<TreeNode> next = new Stack<>();
        Stack<TreeNode> prev = new Stack<>();
        while (root != null) {
            if (root.val > target) {
                next.push(root);
                root = root.left;
            } else {
                prev.push(root);
                root = root.right;
            }
        } 
        
        while (res.size() < k) {
            double distNext = next.isEmpty() ? Double.MAX_VALUE : Math.abs(next.peek().val - target);
            double distPrev = prev.isEmpty() ? Double.MAX_VALUE : Math.abs(prev.peek().val - target);
            
            if (distNext < distPrev) {
                res.add(next.peek().val);
                updateNext(next);
            } else {
                res.add(prev.peek().val);
                updatePrev(prev);
            }
        }
        
        return res;
    }
    
    public void updateNext(Stack<TreeNode> stk) {
        TreeNode node = stk.pop().right;
        
        while (node != null) {
            stk.push(node);
            node = node.left;
        }
    }
    
    public void updatePrev(Stack<TreeNode> stk) {
        TreeNode node = stk.pop().left;
        
        while (node != null) {
            stk.push(node);
            node = node.right;
        }
    }
}
```
{% endtab %}
{% endtabs %}

