# validate binary search tree

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys **less than** the node's key.
* The right subtree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right subtrees must also be binary search trees.
* A single node tree is a BST.

{% tabs %}
{% tab title="Notes" %}
* Two methods: 

1. inorder traversal\(recur and iterative\)
2. divide and conquer
{% endtab %}

{% tab title="Solution" %}
```java
//traverse 
public class Solution {
    //recur
    public TreeNode lastNode;
    public boolean isValid;
    
    public boolean isValidBST(TreeNode root) {
        isValid = true;
        lastNode = null;
        
        inorderTraverse(root);
        return isValid;
    }
    
    public void inorderTraverse(TreeNode root) {
        if (root == null) {
            return;
        }
        
        inorderTraverse(root.left);
        if (lastNode != null && lastNode.val >= root.val) {
            isValid = false;
        }
        lastNode = root; //!!!
        inorderTraverse(root.right);
    }
    
    //iterative
    public boolean isValidBST(TreeNode root) {        
        TreeNode node = root;
        Stack<TreeNode> stack = new Stack<>();
        while (node != null) {
            stack.push(node);
            node = node.left;
        }

        TreeNode lastNode = null;
        while (!stack.isEmpty()) {
            node = stack.pop();
            if (lastNode != null && lastNode.val >= node.val) {
                return false;
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

    return true;
    }
}

//dc
class ResultType {
    public boolean isBST;
    public TreeNode minNode, maxNode;
    public ResultType(boolean isBST) {
        this.isBST = isBST;
        this.minNode = null;
        this.maxNode = null;
    }
}

public class Solution {
    public boolean isValidBST(TreeNode root) {
        return divideConquer(root).isBST;
    }
    
    public ResultType divideConquer(TreeNode root) {
        if (root == null) {
            return new ResultType(true);
        }
        
        ResultType left = divideConquer(root.left);
        ResultType right = divideConquer(root.right);
        if (!left.isBST || !right.isBST) {
            return new ResultType(false);
        }
        
        if ((left.maxNode != null && left.maxNode.val >= root.val) || 
            (right.minNode != null && right.minNode.val <= root.val)) {
            return new ResultType(false);
        }
        
        //isBST
        ResultType result = new ResultType(true);
        result.maxNode = right.maxNode != null ? right.maxNode : root;
        result.minNode = left.minNode != null ? left.minNode : root;
        
        return result;
    }
}
```
{% endtab %}
{% endtabs %}

