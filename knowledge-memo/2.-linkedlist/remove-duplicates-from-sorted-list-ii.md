---
description: >-
  Given a sorted linked list, delete all nodes that have duplicate numbers,
  leaving only distinct numbers from the original list.
---

# remove duplicates from sorted list II

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public ListNode deleteDuplicates(ListNode head) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode node = dummy;

    while (node.next != null && node.next.next != null) {
        if (node.next.val == node.next.next.val) {
            int val = node.next.val;
            while (node.next != null && node.next.val == val) {
                node.next = node.next.next;
            }
        } else {
            node = node.next;
        }
    }

    return dummy.next;
}
```
{% endtab %}
{% endtabs %}

