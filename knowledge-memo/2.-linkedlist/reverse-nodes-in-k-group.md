# Reverse Nodes in k-group

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
// constant space
public ListNode reverseKGroup(ListNode head, int k) {
    if (head == null || k <= 1) {
        return head;
    }

    ListNode dummy = new ListNode(0), prev = dummy, end = prev;
    dummy.next = head;

    while (end.next != null) {
        for (int i = 0; i < k; i++) {
            end = end.next;
            if (end == null) {
                // cannot find n*k any more, so done and return
                return dummy.next;
            }
        }

        // save k+1 node
        ListNode next = end.next;
        // prepare for reverse
        end.next = null;

        // the list to reverse [start, end]
        ListNode start = prev.next;
        // link head and tail (k+1)
        prev.next = reverse(start);
        start.next = next;

        // move to k node and prepare for next round
        prev = start;
        end = prev;
    }

    return dummy.next;
}

public ListNode reverse(ListNode head) {
    ListNode prev = null, cur = head;
    while (cur != null) {
        ListNode tmp = cur.next;
        cur.next = prev;
        prev = cur;
        cur = tmp;
    }

    return prev;
}

// recursive
public ListNode reverseKGroup(ListNode head, int k) {
    if (head == null || k <= 1) {
        return head;
    }

    ListNode dummy = new ListNode(0), prev = head, cur = prev.next;
    dummy.next = head;
    for (int i = 0; i < k - 1; i++) {
        if (cur == null) {
            return head;
        }

        ListNode node = new ListNode(cur.val);
        node.next = dummy.next;
        dummy.next = node;
        prev = cur;
        cur = cur.next;
    }

    head.next = reverseKGroup(cur, k);

    return dummy.next;
}
```
{% endtab %}
{% endtabs %}
