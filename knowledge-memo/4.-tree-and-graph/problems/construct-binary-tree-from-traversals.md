# construct binary tree from traversals

## I from Inorder and Postorder Traversal

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param inorder: A list of integers that inorder traversal of a tree
     * @param postorder: A list of integers that postorder traversal of a tree
     * @return: Root of a tree
     */
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || postorder == null || inorder.length != postorder.length) {
            return null;
        }
        
        TreeNode root = helper(inorder, 0, inorder.length - 1, postorder, 0, postorder.length - 1);
        return root;
    }
    
    public TreeNode helper(int[] inorder, int inStart, int inEnd, int[] postorder,
        int postStart, int postEnd) {
            if (inStart > inEnd) {
                return null;
            }
            
            TreeNode root = new TreeNode(postorder[postEnd]);
            int index = 0;
            for (int i = inStart; i <= inEnd; i++) {
                if (inorder[i] == root.val) {
                    index = i;
                    break;
                }
            }
            
            //inorder
            //inStart ... index ... inEnd
            //#index - inStart
            //postorder
            //postStart ... ... postEnd
            //left.end - > postStart + index - instart - 1

            root.left = helper(inorder, inStart, index - 1, postorder, postStart, postStart + index - inStart - 1);
            root.right = helper(inorder, index + 1, inEnd, postorder, postStart + index - inStart, postEnd - 1);
            
            return root;
        }
}
```
{% endtab %}
{% endtabs %}

## II from Inorder and Preorder Traversal

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param inorder: A list of integers that inorder traversal of a tree
     * @param preorder: A list of integers that preorder traversal of a tree
     * @return: Root of a tree
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder == null || inorder == null || preorder.length != inorder.length) {
            return null;
        }
        
        TreeNode root = helper(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1);

        return root;
    }
    
    public TreeNode helper(int[] preorder, int preStart, int preEnd, int[] inorder,
        int inStart, int inEnd) {
        if (inStart > inEnd) {
            return null;
        }
        
        TreeNode root = new TreeNode(preorder[preStart]);
        int index = 0;
        for (int i = inStart; i <= inEnd; i++) {
            if (inorder[i] == root.val) {
                index = i;
                break;
            }
        }
        
        //preorder
        //preStart ... ... preEnd
        //left.end - > preStart + 1 - index - inStart - 1
        
        //inorder
        //inStart ... index ... inEnd
        //#index - instart
        
        root.left = helper(preorder, preStart + 1, preStart + index - inStart, inorder, inStart, index - 1);
        root.right = helper(preorder, preStart + index - inStart + 1, preEnd, inorder, index + 1, inEnd);
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}

