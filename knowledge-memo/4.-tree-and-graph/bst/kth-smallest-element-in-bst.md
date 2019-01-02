# kth smallest element in bst

Given a binary search tree, write a function `kthSmallest` to find the kth smallest element in it.

{% tabs %}
{% tab title="Notes" %}
* inorder traversal: recursive, iterative O\(k\), O\(h\)
* Follow up: 

What if the BST is modified \(insert/delete operations\) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

1. add a field "counter" to represent the \# of nodes rooted at certain node, or use a hashmap to store this information
2. record the nodes in the affected path when insert/delete operations happen and make corresponding updates
3. use quick select to find the kth smallest element, O\(h\)
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param root: the given BST
     * @param k: the given k
     * @return: the kth smallest element in BST
     */
    
    //recur
    public int count;
    public int kthSmallestVal;
    public int kthSmallest(TreeNode root, int k) {
        count = k;
        traverse(root);
        return kthSmallestVal;
    }
    
    public void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        
        if (count > 0) {
            traverse(root.left);
            count--;
            if (count == 0) {
                kthSmallestVal = root.val;
                return;
            }
            traverse(root.right);
        }
    }
    
    
    //iterative 
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        
        int count = 0;
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (++count == k) {
                return node.val;
            }
            if (node.right != null) {
                node = node.right;
                while (node != null) {
                    stack.push(node);
                    node = node.left;
                }
            }
        }
        
        return -1;
    }
    
    //follow up
    public Map<TreeNode, Integer> map;
    public int kthSmallest(TreeNode root, int k) {
        map = new HashMap<>();
        countNode(root);
        
        return quickSelect(root, k);
    }
    
    
    public int countNode(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int left = countNode(root.left);
        int right = countNode(root.right);
        map.put(root, left + right + 1);
        
        return left + right + 1;
    }
    
    public int quickSelect(TreeNode root, int k) {
        int left = root.left == null ? 0 : map.get(root.left);
        
        if (left + 1 == k) {
            return root.val;
        } else if (left + 1 < k) {
            return kthSmallest(root.right, k - left - 1);
        }
        
        return kthSmallest(root.left, k);
    }
}
```
{% endtab %}
{% endtabs %}

