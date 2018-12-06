# binary tree paths

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recur 
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        dfs(root, res, "");
        return res;
    }
    
    public void dfs(TreeNode node, List<String> res, String s) {
        if (node.left == null && node.right == null) {
            res.add(s + node.val);
            return;
        }
        
        if (node.left != null) {
            dfs(node.left, res, s + node.val + "->");
        }
        
        if (node.right != null) {
            dfs(node.right, res, s + node.val + "->");
        }
    }
    
    //iterative bfs
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        Queue<String> strQueue = new LinkedList<>();
        Queue<TreeNode> nodeQueue = new LinkedList<>();
        strQueue.offer("");
        nodeQueue.offer(root);
        while (!nodeQueue.isEmpty()) {
            TreeNode node = nodeQueue.poll();
            String str = strQueue.poll();
            if (node.left == null && node.right == null) {
                res.add(str + node.val);
            }
            
            if (node.left != null) {
                nodeQueue.offer(node.left);
                strQueue.offer(str + node.val + "->");
            }
            
            if (node.right != null) {
                nodeQueue.offer(node.right);
                strQueue.offer(str + node.val + "->");
            }
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

