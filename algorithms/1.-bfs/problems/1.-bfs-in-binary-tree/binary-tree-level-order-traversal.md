# binary tree level order traversal I && II

## I

Given a binary tree, return the level order traversal of its nodes' values. \(ie, from left to right, level by level\).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```text
[
  [3],
  [9,20],
  [15,7]
]
```

{% tabs %}
{% tab title="Note" %}
* level information: extra loop!
* bfs and dfs implementation ways
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //bfs
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            
            res.add(level);
        }
        
        return res;
    }
    
    //dfs
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        dfs(root, res, 0);
        
        return res;
    }
    
    public void dfs(TreeNode root, List<List<Integer>> res, int level) {
        if (root == null) {
            return;
        }
        
        if (level == res.size()) {
            res.add(new ArrayList<>());
        }
        
        res.get(level).add(root.val);
        
        dfs(root.left, res, level + 1);
        dfs(root.right, res, level + 1);
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a binary tree, return the bottom-up level order traversal of its nodes' values. \(ie, from left to right, level by level from leaf to root\).

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //bfs
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        
        if (root == null) {
            return res;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            List<Integer> level = new ArrayList<>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            res.add(0, level);
        }
        
        return res;
    }
    
    //dfs
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        
        dfs(root, res, 0);
        
        return res;
    }
    
    public void dfs(TreeNode root, List<List<Integer>> res, int level) {
        if (root == null) {
            return;
        }
        
        if (level == res.size()) {
            res.add(0, new ArrayList<>());
        }
        
        dfs(root.left, res, level + 1);
        dfs(root.right, res, level + 1);
        res.get(res.size() - 1 - level).add(root.val);
    }
}
```
{% endtab %}
{% endtabs %}

