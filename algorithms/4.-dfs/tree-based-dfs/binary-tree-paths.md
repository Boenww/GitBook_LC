# binary tree paths

Given a binary tree, return all root-to-leaf paths.

{% tabs %}
{% tab title="Notes" %}
* traverse 
* dc
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //traverse
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
        if (node == null) {
            return;
        }
        
        if (node.left == null && node.right == null) {
            res.add(s + node.val);
            return;
        }
                
        dfs(node.left, res, s + node.val + "->");
        dfs(node.right, res, s + node.val + "->");
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
    
    //dc
    public List<String> binaryTreePaths(TreeNode root) {
        if (root == null) {
            return new ArrayList<>();
        }

        List<String> left = binaryTreePaths(root.left);
        List<String> right = binaryTreePaths(root.right);

        List<String> res = new ArrayList<>();
        for (String path: left) {
            res.add(root.val + "->" + path);
        }

        for (String path: right) {
            res.add(root.val + "->" + path);
        }
        
        //take care for the leaf node
        if (res.size() == 0) {
            res.add(root.val + "");
        }

        return res;
    }
}
```
{% endtab %}
{% endtabs %}

