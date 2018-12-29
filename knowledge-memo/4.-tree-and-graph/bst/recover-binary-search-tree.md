# recover binary search tree

In a binary search tree, \(Only\) two nodes are swapped. Find out these nodes and swap them. If there is no node swapped, return original root of tree.

{% tabs %}
{% tab title="Notes" %}
* Constant space: Morris?
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //iterative
    public void recoverTree(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        
        TreeNode node = root;
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
        
        TreeNode lastNode = null, firstNode = null, secondNode = null;
        while (!stack.isEmpty()) {
            node = stack.pop();
            if (firstNode == null && lastNode != null && node.val < lastNode.val) {
                firstNode = lastNode;
            }
            
            if (firstNode != null && node.val < lastNode.val) {
                secondNode = node;
            }
            lastNode = node;
            
            if (node.right != null) {
                node = node.right;
                while (node != null) {
                    stack.push(node);
                    node = node.left;
                }
            }
        }
        
        if (firstNode != null) {
            int tmp = firstNode.val;
            firstNode.val = secondNode.val;
            secondNode.val = tmp;
        }
    }
    
    //recursive
    public TreeNode lastNode = null, firstNode = null, secondNode = null;
    
    public void recoverTree(TreeNode root) {
        inorderTraverse(root);
        
        if (firstNode != null) {
            int tmp = firstNode.val;
            firstNode.val = secondNode.val;
            secondNode.val = tmp;
        }
    }
    
    public void inorderTraverse(TreeNode root) {
        if (root == null) {
            return;
        }
        
        inorderTraverse(root.left);
        if (firstNode == null && lastNode != null && root.val < lastNode.val) {
            firstNode = lastNode;
        }
        
        if (firstNode != null && root.val < lastNode.val) {
            secondNode = root;
        }
        lastNode = root;
        inorderTraverse(root.right);
    }
}


```
{% endtab %}
{% endtabs %}

