---
description: 'Given a binary tree, return the required traversal of its nodes'' values.'
---

# traversal

## Preorder

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//recur
public List<Integer> preorderTraversal(TreeNode root) { 
    List<Integer> res = new ArrayList<>();
    helper(root, res);
    
    return res;
}

public void helper(TreeNode node, List<Integer> res) {
    if (node == null) {
        return;
    }
    
    res.add(node.val);
    helper(node.left, res);
    helper(node.right, res);
}

//iterative
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) { //!!! o.w. runtime error
        return res;
    }
    
    Stack<TreeNode> stk = new Stack<>();
    stk.push(root);
    
    while (!stk.isEmpty()) {
        TreeNode node = stk.pop();
        res.add(node.val);
        
        if (node.right != null) {
            stk.push(node.right);
        }
        
        if (node.left != null) {
            stk.push(node.left);
        }
    }
    
    return res;
}
```
{% endtab %}
{% endtabs %}

## Inorder

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//recursive
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    helper(root, res);
    
    return res;
}

public void helper(TreeNode node, List<Integer> res) {
    if (node == null) {
        return;
    }
    
    helper(node.left, res);
    res.add(node.val);
    helper(node.right, res);
}

//iterative
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    Stack<TreeNode> stk = new Stack<>();
    while (root != null) {
        stk.push(root);
        root = root.left;
    }
    
    while (!stk.isEmpty()) {
        TreeNode node = stk.pop();
        res.add(node.val);
            
        node = node.right;
        while (node != null) {
            stk.push(node);
            node = node.left;
        }
    }
    
    return res;
}
```
{% endtab %}
{% endtabs %}

## Postorder

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//recursive
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    helper(root, res);
    
    return res;
}

public void helper(TreeNode node, List<Integer> res) {
    if (node == null) {
        return;
    }
    
    helper(node.left, res);
    helper(node.right, res);
    res.add(node.val);
}

//iterative
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if (root == null) {
        return res;
    }
    
    Stack<TreeNode> stk = new Stack<>();
    stk.push(root);
    
    while (!stk.isEmpty()) {
        TreeNode node = stk.pop();
        res.add(0, node.val);
        
        if (node.left != null) {
            stk.push(node.left);
        }
        
        if (node.right != null) {
            stk.push(node.right);
        }
    }
    
    return res;
}
```
{% endtab %}
{% endtabs %}

