---
description: >-
  Given two non-empty binary trees s and t, check whether tree t has exactly the
  same structure and node values with a subtree of s.
---

# subtree of another tree

{% tabs %}
{% tab title="Notes" %}
* Compare preorder strings -&gt; possible O\(n\)
* Recursive with same tree check
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //compare preorder string
    public boolean isSubtree(TreeNode s, TreeNode t) {
        String sPreorder = getPreorder(s); 
        String tPreorder = getPreorder(t);
        
        return sPreorder.contains(tPreorder);
    }
    
    public String getPreorder(TreeNode s){
        StringBuilder sb = new StringBuilder();
        Stack<TreeNode> stk = new Stack();
        stk.push(s);
        while(!stk.isEmpty()){
           TreeNode node = stk.pop();
          if (node == null) {
              sb.append(",#");
          } else {
              sb.append("," + node.val);
          }
             
           if(node != null){
                stk.push(node.right);    
                stk.push(node.left);  
           }
        }
        return sb.toString();
    }
    
    //recursive with same tree check
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null) {
            return t == null;
        }
        
        return isIdentical(s, t) || isSubtree(s.left, t) || isSubtree(s.right, t);
    }
    
    public boolean isIdentical(TreeNode s, TreeNode t) {
        if (s == null && t == null) {
            return true;
        } else if (s == null || t == null || s.val != t.val) {
            return false;
        } 
        
        return isIdentical(s.left, t.left) && isIdentical(s.right, t.right);
    }
      
}
```
{% endtab %}
{% endtabs %}

