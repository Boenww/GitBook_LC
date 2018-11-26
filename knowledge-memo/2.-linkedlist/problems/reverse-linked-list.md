# reverse linked list

{% tabs %}
{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param head: n
     * @return: The new head of reversed linked list.
     */
    //recursive
    public ListNode reverse(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode p = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return p;
    }
    
    //iterative
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
}
```
{% endtab %}
{% endtabs %}

