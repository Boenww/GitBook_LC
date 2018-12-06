---
description: >-
  Given a binary tree, collect a tree's nodes as if you were doing this: Collect
  and remove all leaves, repeat until the tree is empty.
---

# find leaves of binary tree

{% tabs %}
{% tab title="Notes" %}
* Group the nodes with the same height.
* Height definition here is the number of edges from the node to the leaf of that branch.
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        getHeight(root, res);
        
        return res;
    }
    
    public int getHeight(TreeNode node, List<List<Integer>> res) {
        if (node == null) {
            return 0;
        }
        
        int left = getHeight(node.left, res);
        int right = getHeight(node.right, res);
        int index = Math.max(left, right);
        if (res.size() == index) {
            res.add(new ArrayList<>());
        }
        res.get(index).add(node.val);
        
        return index + 1;
    }
}
```
{% endtab %}
{% endtabs %}

