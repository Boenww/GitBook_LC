# remove nth node from end

{% tabs %}
{% tab title="Notes" %}
* The case to remove the head node
{% endtab %}

{% tab title="Solution" %}
```java
public ListNode removeNthFromEnd(ListNode head, int n) {        
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode slow = dummy, fast = head;
    for (int i = 0; i < n; i++) {
        if (fast == null) {
            return null;
        }

        fast = fast.next;
    }

    while (fast != null) {
        fast = fast.next;
        slow = slow.next;
    }

    slow.next = slow.next.next;

    return dummy.next;
}
```
{% endtab %}
{% endtabs %}

