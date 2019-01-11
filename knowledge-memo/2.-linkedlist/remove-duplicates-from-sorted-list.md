# remove duplicates from sorted list I && II

## I

Given a sorted linked list, delete all duplicates such that each element appear only once.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode node = head;
        while (node.next != null) {
            if (node.val == node.next.val) {
                node.next = node.next.next;
            } else {
                node = node.next;
            }
        }
        
        return head;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

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

