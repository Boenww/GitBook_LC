---
description: >-
  Given the root and two nodes in a Binary Tree. Find the lowest common
  ancestor(LCA) of the two nodes.
---

# lowest common ancestor

{% tabs %}
{% tab title="Notes" %}
* LCA of BST
* Easy version: The node has an extra attribute `parent` which point to the father of itself. The root's parent is null. can use the similar algorithm for finding the intersection of two linked lists.
* 
{% endtab %}

{% tab title="Solution" %}
```java
//LCA of BST


//Easy version 
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

