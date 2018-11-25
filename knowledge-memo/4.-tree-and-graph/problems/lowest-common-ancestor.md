---
description: >-
  Given the root and two nodes in a Binary Tree. Find the lowest common
  ancestor(LCA) of the two nodes.
---

# lowest common ancestor

{% tabs %}
{% tab title="Notes" %}
LCA of BST
{% endtab %}

{% tab title="Solution" %}
```java
//LCA of BST
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
    //recursive
    if (root == null) {
        return null;
    }

    if ((root.val - A.val) * (root.val - B.val) > 0) {
        if (root.val > A.val) {
            return lowestCommonAncestor(root.left, A, B);
        } else {
            return lowestCommonAncestor(root.right, A, B);
        }
    } 
        
    return root;
        
    //iterative
    //root == null
    while ((root.val - A.val) * (root.val - B.val) > 0) {
        if (root.val > A.val) {
            root = root.left;
        } else {
            root = root.right;
        }
    }
        
    return root;
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Notes" %}
Easy version: The node has an extra attribute `parent` which point to the father of itself. The root's parent is null. can use the similar algorithm for finding the intersection of two linked lists.
{% endtab %}

{% tab title="Solution" %}
```java
public ParentTreeNode lowestCommonAncestorII(ParentTreeNode A, ParentTreeNode B) {
        Set<ParentTreeNode> parentSet = new HashSet<>();
        ParentTreeNode cur = A;
        while (cur != null) {
            parentSet.add(cur);
            cur = cur.parent;
        }
        
        cur = B;
        while (cur != null) {
            if (parentSet.contains(cur)) {
                return cur;
            }
            cur = cur.parent;
        }
        
        return null;
        
        //intersection method
        ParentTreeNode a = A, b = B;
        while (a != b) {
            a = a.parent == null ? B : a.parent;
            b = b.parent == null ? A : b.parent;
        }
        
        return a;
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Notes" %}
Assume two nodes are exist in tree.
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //recursive
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left != null && right != null) {
            return root;
        } else if (left != null) {
            return left;
        }
        
        return right;
    }
    
    //iterative
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Map<TreeNode, TreeNode> parent = new HashMap<>();
        Stack<TreeNode> stk = new Stack<>();
        stk.push(root);
        parent.put(root, null);

        //find both p's and q's parents
        while (!parent.containsKey(p) || !parent.containsKey(q)) {
            TreeNode node = stk.pop();
            if (node.left != null) {
                parent.put(node.left, node);
                stk.push(node.left);
            }

            if (node.right != null) {
                parent.put(node.right, node);
                stk.push(node.right);
            }
        }

        //find a path from p to the root
        Set<TreeNode> path = new HashSet<>();
        TreeNode P = p, Q = q;
        while (P != null) {
            path.add(P);
            P = parent.get(P);
        }

        //find q or first q's ancestor in this path
        while (!path.contains(Q)) {
            Q = parent.get(Q);
        }

        return Q;
    }
}
```
{% endtab %}
{% endtabs %}

