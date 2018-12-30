# two sum IV - input is a bst

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

{% tabs %}
{% tab title="Notes" %}
* Using a hashset or binary search after an inorder traversal
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //hashset
    public boolean isFound;
    
    public boolean findTarget(TreeNode root, int k) {
        inorderTraverse(root, k, new HashSet<>());
        return isFound;
    }
    
    public void inorderTraverse(TreeNode root, int k, Set<Integer> set) {
        if (root == null) {
            return;
        }
        
        inorderTraverse(root.left, k, set);
        if (set.contains(k - root.val)) {
            isFound = true;
            return;
        }
        set.add(root.val);
        inorderTraverse(root.right, k, set);
    }
    
    //
    public boolean findTarget(TreeNode root, int k) {
        List<Integer> traversal = new ArrayList<>();
        
        inorderTraverse(root, traversal);
        int left = 0, right = traversal.size() - 1;
        while (left < right) {
            if (traversal.get(left) + traversal.get(right) == k) {
                return true;
            } else if (traversal.get(left) + traversal.get(right) < k) {
                left++;
            } else {
                right--;
            }
        }
        
        return false;
    }
    
    public void inorderTraverse(TreeNode root, List<Integer> traversal) {
        if (root == null) {
            return;
        }
        
        inorderTraverse(root.left, traversal);
        traversal.add(root.val);
        inorderTraverse(root.right, traversal);
    }
}
```
{% endtab %}
{% endtabs %}

