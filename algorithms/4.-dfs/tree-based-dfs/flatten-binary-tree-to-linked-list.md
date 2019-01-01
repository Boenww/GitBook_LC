# flatten binary tree to linked list

Given a binary tree, flatten it to a linked list in preorder traversal in-place. Here we use the _right_ pointer in TreeNode as the _next_ pointer in ListNode.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //traverse
    public TreeNode lastNode = null;
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        
        if (lastNode != null) {
            lastNode.left = null;
            lastNode.right = root;
        }
        
        lastNode = root;
        TreeNode right = root.right;
        flatten(root.left);
        flatten(right);
    }
    
    //iterative
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
    
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node.right != null) {
                stack.push(node.right);
            }
            
            if (node.left != null) {
                stack.push(node.left);
            }
            
            node.left = null;
            if (!stack.isEmpty()) { //!EmptyStackException
                node.right = stack.peek();    
            }
        }
    }
    
    //dc
    public void flatten(TreeNode root) {
        helper(root);
    }    
    
    public TreeNode helper(TreeNode root) {
        if (root == null) {
            return root;
        }
        
        TreeNode left = helper(root.left);
        TreeNode right = helper(root.right);
        
        root.right = left;
        root.left = null;
        
        TreeNode node = root; //!!!
        while (node.right != null) {
            node = node.right;
        }
        
        node.right = right;
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}

