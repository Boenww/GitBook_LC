---
description: >-
  Given a Binary Search Tree (BST), convert it to a Greater Tree such that every
  key of the original BST is changed to the original key plus sum of all keys
  greater than the original key in BST.
---

# convert bst to greater tree

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    private int sum = 0;
    public TreeNode convertBST(TreeNode root) {
        if (root == null) {
            return null;
        }
        
        convertBST(root.right);
        sum += root.val;
        root.val = sum;
        convertBST(root.left);
        
        return root;
    }
    
    //iterative
    public TreeNode convertBST(TreeNode root) {
        int sum = 0;
        Stack<TreeNode> stk = new Stack<>();
        TreeNode node = root;
        while (node != null) {
            stk.push(node);
            node = node.right;
        }
        
        while (!stk.isEmpty()) {
            TreeNode cur = stk.pop();
            sum += cur.val;
            cur.val = sum;
            if (cur.left != null) {
                cur = cur.left;
                while (cur != null) {
                    stk.push(cur);
                    cur = cur.right;
                }
            }
        }
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}

