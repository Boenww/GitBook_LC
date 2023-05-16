---
description: lintcode
---

# 492. implement queue by linked list

Implement a Queue by linked list. Support the following basic methods:

1. `enqueue(item)`. Put a new item in the queue.
2. `dequeue()`. Move the first item out of the queue, return it.

{% tabs %}
{% tab title="Notes" %}
* dummy and tail
{% endtab %}

{% tab title="Solution" %}
```java
class ListNode {
    public int val; 
    public ListNode next;
    public ListNode(int val) {
        this.val = val;
    }
}

public class MyQueue {
    public ListNode dummy, tail;
    
    public MyQueue() {
        dummy = new ListNode(0);
        tail = dummy;
    }
    
    public void enqueue(int item) {
        ListNode node = new ListNode(item);
        tail.next = node;
        tail = tail.next;
    }

    public int dequeue() {
        if (dummy.next == null) {
            return -1;
        }
        int res = dummy.next.val;
        dummy.next = dummy.next.next;
        if (dummy.next == null) {
            tail = dummy;
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Implement a deque

{% tabs %}
{% tab title="Notes" %}
* single linked list -> pop\_back() is O(n)
* double linked list
{% endtab %}

{% tab title="Solution" %}
```java
class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int val) {
        this.val = val;
    }
}

public class Dequeue {
    public ListNode dummy, tail;
    
    public Dequeue() {
        dummy = new ListNode(0);
        tail = dummy;
    }

    public void push_front(int item) {
        ListNode node = new ListNode(item);
        node.next = dummy.next;
        dummy.next = node;
        if (tail == dummy) { // !!!
            tail = tail.next;
        }
    }

    public void push_back(int item) {
        ListNode node = new ListNode(item);
        tail.next = node;
        tail = tail.next;
    }

    public int pop_front() {
        int res = dummy.next.val;
        dummy.next = dummy.next.next;
        if (dummy.next == null) {
            tail = dummy;
        }
        
        return res;
    }

    public int pop_back() {
        int res = tail.val;
        ListNode cur = dummy;
        while (cur.next != tail) {
            cur = cur.next;
        }
        
        cur.next = cur.next.next;
        tail = cur; // !!!
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}
