# merge two binary trees

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
// recursive
public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
    if (t1 == null) {
        return t2;
    }
    if (t2 == null) {
        return t1;
    }
    
    TreeNode root = new TreeNode(t1.val + t2.val);
    root.left = mergeTrees(t1.left, t2.left);
    root.right = mergeTrees(t1.right, t2.right);
    return root;
}

// iterative 1
public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
	if (t1 == null) {
		return t2;
	}

	Stack<TreeNode[]> stk = new Stack<>();
	stk.push(new TreeNode[]{t1, t2});
	while (!stk.isEmpty()) {
		TreeNode[] t = stk.pop();
		if (t[0] == null || t[1] == null) {
			continue;
		}

		t[0].val += t[1].val;
		if (t[0].left == null) {
			t[0].left = t[1].left;
		} else {
			stk.push(new TreeNode[]{t[0].left, t[1].left});
		}

		if (t[0].right == null) {
			t[0].right = t[1].right;
		} else {
			stk.push(new TreeNode[]{t[0].right, t[1].right});
		}
	}

	return t1;
}

// iterative 2
public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
    // Write your code here
    if (t1 == null) {
        return t2;
    }

    if (t2 == null) {
        return t1;
    }

    TreeNode root = new TreeNode(t1.val + t2.val);
    Queue<TreeNode> queue = new LinkedList<>();
    Queue<TreeNode> queue1 = new LinkedList<>();
    Queue<TreeNode> queue2 = new LinkedList<>();
    queue.offer(root);
    queue1.offer(t1);
    queue2.offer(t2);
    while (!queue.isEmpty()) {
        TreeNode node = queue.poll(), node1 = queue1.poll(), node2 = queue2.poll();

        mergeNode(node, node1, node2, queue, queue1, queue2);
    }

    return root;
}

public void mergeNode(TreeNode mergeNode, TreeNode node1, TreeNode node2, Queue<TreeNode> queue,
    Queue<TreeNode> queue1, Queue<TreeNode> queue2) {
    if (node1.left != null && node2.left != null) {
        mergeNode.left = new TreeNode(node1.left.val + node2.left.val);
        queue.offer(mergeNode.left);
        queue1.offer(node1.left);
        queue2.offer(node2.left);
    } else if (node1.left != null) {
        mergeNode.left = node1.left;
    } else {
        mergeNode.left = node2.left;
    }

    if (node1.right != null && node2.right != null) {
        mergeNode.right = new TreeNode(node1.right.val + node2.right.val);
        queue.offer(mergeNode.right);
        queue1.offer(node1.right);
        queue2.offer(node2.right);
    } else if (node1.right != null) {
        mergeNode.right = node1.right;
    } else {
        mergeNode.right = node2.right;
    }        
}
```
{% endtab %}
{% endtabs %}
