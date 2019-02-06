# construct binary tree from traversals

## 106. from Inorder and Postorder Traversal

{% tabs %}
{% tab title="Notes" %}
* The search for root in inorder array can be optimized with building a hashmap.
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

## 105. from Inorder and Preorder Traversal

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

## 889. from Preorder and Postorder Traversal

{% tabs %}
{% tab title="Notes" %}
* Difference: should take care when the last left root node appears.
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public TreeNode constructFromPrePost(int[] pre, int[] post) {
        return helper(pre, 0, pre.length - 1, post, 0, post.length - 1);
    }
    
    public TreeNode helper(int[] pre, int preStart, int preEnd, int[] post, int postStart,
                          int postEnd) {
        if (preStart > preEnd) {
            return null;
        }
        
        if (preStart == preEnd) { //!!! last left root -> o.w. cannot find next left root in post -> index = 0, preStart + 1
            return new TreeNode(pre[preStart]);
        }
        
        TreeNode root = new TreeNode(pre[preStart]);
        int index = 0;
        for (int i = postStart; i <= postEnd; i++) {
            if (post[i] == pre[preStart + 1]) { //root of left subtree
                index = i;
                break;
            }
        }
        
        //pre
        //preStart ... ... preEnd
        //left.end -> preStart + 1 + index - postStart
        //post
        //postStart ... ... postEnd
        //#index - postStart + 1
        root.left = helper(pre, preStart + 1, preStart + 1 + index - postStart, post, postStart, index);
        root.right = helper(pre, preStart + 2 + index - postStart, preEnd, post, index + 1, postEnd - 1);
        
        return root;
    }
}

//!!!
//pre, 1, 3, post, 0, 2
//index = 0

//pre, 2, 2, post, 0, 0
//index = 0

//pre, 3, 3, post, 0, 0
//pre, 4, 4, post, 0, 0
//... ArrayIndexOutOfBounds


//iterative 
public TreeNode constructFromPrePost(int[] pre, int[] post) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode root = new TreeNode(pre[0]);
        stack.push(root);
        for (int i = 1, j = 0; i < pre.length; ++i) {
            TreeNode node = new TreeNode(pre[i]);
            while (stack.peek().val == post[j]) {
                stack.pop();
                j++;
            }
            
            if (stack.peek().left == null) {
                stack.peek().left = node;
            } else {
                stack.peek().right = node;
            }
            
            stack.push(node);
        }
        
        return root;
}
```
{% endtab %}
{% endtabs %}

