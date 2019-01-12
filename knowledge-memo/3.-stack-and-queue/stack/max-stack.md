# max stack

Design a max stack that supports push, pop, top, peekMax and popMax.

1. push\(x\) -- Push element x onto stack.
2. pop\(\) -- Remove the element on top of the stack and return it.
3. top\(\) -- Get the element on the top.
4. peekMax\(\) -- Retrieve the maximum element in the stack.
5. popMax\(\) -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

{% tabs %}
{% tab title="Notes" %}
* two stacks: popMax\(\) is O\(n\) and O\(1\) for the other operations
* double linked list with treemap: all O\(logn\) except top\(\) 
{% endtab %}

{% tab title="Solution" %}
```java
//1
class MaxStack {
    public Stack<Integer> maxStack;
    public Stack<Integer> stack;
    
    public MaxStack() {
        maxStack = new Stack<>();
        stack = new Stack<>();
    }
    
    public void push(int x) {
        if (maxStack.isEmpty()) {
            maxStack.push(x);
        } else {
            maxStack.push(peekMax() > x ? peekMax() : x);
        }

        stack.push(x);
    }
    
    public int pop() {
        maxStack.pop();
        
        return stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int peekMax() {
        return maxStack.peek();
    }
    
    public int popMax() {
        int max = peekMax();
        Stack<Integer> buffer = new Stack<>();
        while (top() != peekMax()) {
            buffer.push(pop());
        }
        pop();
        while (!buffer.isEmpty()) {
            push(buffer.pop());
        }
        
        return max;
    }
}

//2
class MaxStack {
    public DoubleLinkedList dList;
    public TreeMap<Integer, List<ListNode>> map;
    
    public MaxStack() {
        dList = new DoubleLinkedList();
        map = new TreeMap<>();
    }
    
    public void push(int x) {
        ListNode node = dList.add(x);
        map.putIfAbsent(x, new ArrayList<>());
        map.get(x).add(node);
    }
    
    public int pop() {
        int key = dList.pop();
        List<ListNode> list = map.get(key);
        list.remove(list.size() - 1);
        if (list.isEmpty()) {
            map.remove(key);
        }
        
        return key;
    }
    
    public int top() {
        return dList.peek();
    }
    
    public int peekMax() {
        return map.lastKey(); //also O(logN)
    }
    
    public int popMax() {
        int max = peekMax();
        List<ListNode> list = map.get(max);
        ListNode node = list.remove(list.size() - 1);
        if (list.isEmpty()) {
            map.remove(max);
        }
        dList.remove(node);
        return max;
    }
}

class DoubleLinkedList {
    public ListNode head, tail;
    
    public DoubleLinkedList() {
        head = new ListNode(0);
        tail = new ListNode(0);
        tail.prev = head;
        head.next = tail;
    }
    
    public ListNode add(int val) {
        ListNode node = new ListNode(val);
        node.next = tail;
        tail.prev.next = node;
        node.prev = tail.prev;
        tail.prev = node;
        return node;
    }
    
    public int pop() {
        return remove(tail.prev).val;
    }
    
    public ListNode remove(ListNode node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
        
        return node;
    }
    
    public int peek() {
        return tail.prev.val;
    }
}

class ListNode {
    public int val;
    public ListNode next, prev;
    public ListNode(int val) {
        this.val = val;
    }
}
```
{% endtab %}
{% endtabs %}

