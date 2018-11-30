# symmetric tree

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param root: root of the given tree
     * @return: whether it is a mirror of itself 
     */
    //recursive
    public boolean isSymmetric(TreeNode root) {
        return helper(root, root);
    }
    
    public boolean helper(TreeNode node1, TreeNode node2) {
        if (node1 == null && node2 == null) {
            return true;
        }
        
        if (node1 == null || node2 == null) {
            return false;
        }
        
        return node1.val == node2.val && helper(node1.left, node2.right) 
            && helper(node1.right, node2.left);
    }
    
    //iterative O(n), O(n)
    public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode node1 = queue.poll();
            TreeNode node2 = queue.poll();
            if (node1 == null && node2 == null) {
                continue;
            }
            
            if (node1 == null || node2 == null || node1.val != node2.val) {
                return false;
            }
            
            queue.offer(node1.left);
            queue.offer(node2.right);
            queue.offer(node1.right);
            queue.offer(node2.left);
        }
        
        return true;
    }
}
```
{% endtab %}
{% endtabs %}

