# 23. merge k sorted list

Merge _k_ sorted linked lists and return it as one sorted list.

Analyze and describe its complexity.Have you met this question in a real interview?  YesProblem Correction

```
Example:
Given lists:
[
  2->4->null,
  null,
  -1->null
]
```

return `-1->2->4->null`.

{% tabs %}
{% tab title="Notes" %}
* PriorityQueue
* divide and conquer&#x20;
* bottom up
* O(nlogk): n: # of all elements
{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    //pq
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        Queue<ListNode> pq = new PriorityQueue<>(lists.length, new Comparator<ListNode>() {
            @Override
            public int compare(ListNode node1, ListNode node2) {
                return node1.val - node2.val;
            }
        });
        
        for (ListNode node: lists) {
            if (node != null) { //!!!
                pq.add(node);
            }
        }
        
        ListNode dummy = new ListNode(0), tail = dummy;
        
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            
            tail.next = node;
            tail = tail.next;
            if (node.next != null) {
                pq.add(node.next);
            }
        }
        
        return dummy.next;
    }
    
    //dc
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        return helper(lists, 0, lists.length - 1);
    }
    
    public ListNode helper(ListNode[] lists, int start, int end) {
        if (start == end) {
            return lists[start];
        }
        
        int mid = start + (end - start) / 2;
        ListNode left= helper(lists, start, mid);
        ListNode right = helper(lists, mid + 1, end);
        
        return mergeTwoLists(left, right);
    }
    
    public ListNode mergeTwoLists(ListNode head1, ListNode head2) {
        ListNode dummy = new ListNode(0), node = dummy;
        while (head1 != null && head2 != null) {
            if (head1.val < head2.val) {
                node.next = new ListNode(head1.val);
                head1 = head1.next;
            } else {
                node.next = new ListNode(head2.val);
                head2 = head2.next;
            }
            node = node.next;
        }
        
        if (head1 == null) {
            node.next = head2;
        } else {
            node.next = head1;
        }
        
        return dummy.next;
    }
    
    //bottom up
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        List<ListNode> list = new ArrayList<>();
        for (ListNode node: lists) {
            list.add(node);
        }
        
        while (list.size() != 1) {
            List<ListNode> tmp = new ArrayList<>();
            for (int i = 0; i < list.size() - 1; i += 2) {
                tmp.add(mergeTwoLists(list.get(i), list.get(i + 1)));
            }
            
            if (list.size() % 2 == 1) {
                tmp.add(list.get(list.size() - 1));
            }
            list = tmp;
        }
        
        return list.get(0);
    }
}
```
{% endtab %}
{% endtabs %}
