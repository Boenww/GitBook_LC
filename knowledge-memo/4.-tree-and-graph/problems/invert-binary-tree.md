# invert binary tree

{% tabs %}
{% tab title="Notes" %}
* Recursive
* Iterative: level-order traversal to swap the left and right childs of all nodes
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        
        TreeNode left = invertTree(root.right);
        TreeNode right = invertTree(root.left);
        
        root.left = left;
        root.right = right;
        return root;
        
        //or use a helper func
        TreeNode node = root;
        helper(node);
        return root;
    }
    
    public void helper(TreeNode root) {
        if (root == null) {
            return;
        }
        
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        helper(root.left);
        helper(root.right);
    }
    
    //iterative
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        
        // queue or stack doesn't matter
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            
            TreeNode tmp = node.left;
            node.left = node.right;
            node.right = tmp;
            
            if (node.left != null) {
                queue.offer(node.left);
            }
            
            if (node.right != null) {
                queue.offer(node.right);
            }
        }
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}
