# merge two sorted lists

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {     
        ListNode dummy = new ListNode(0), head = dummy, head1 = l1, head2 = l2;
        while (head1 != null && head2 != null) {
            if (head1.val < head2.val) {
                head.next = new ListNode(head1.val);
                head1 = head1.next;
            } else {
                head.next = new ListNode(head2.val);
                head2 = head2.next;
            }
            head = head.next;
        }
        
        while (head1 != null) {
            head.next = new ListNode(head1.val);
            head = head.next;
            head1 = head1.next;
        }
        
        while (head2 != null) {
            head.next = new ListNode(head2.val);
            head = head.next;
            head2 = head2.next;
        }
        
        return dummy.next;
    }
    
    //recursive
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        } else if (l2 == null) {
            return l1;
        }
        
        if (l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```
{% endtab %}
{% endtabs %}

