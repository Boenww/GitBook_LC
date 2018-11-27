# reverse linked list

{% tabs %}
{% tab title="Notes" %}
Follow up: Reverse a linked list from position m to n.
{% endtab %}

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

//Follow up
public ListNode reverseBetween(ListNode head, int m, int n) {
    if (head == null || m >= n) {
        return head;
    }
    
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode preM = dummy;
    
    for (int i = 1; i < m; i++) {
        if (preM == null) {
            return null;
        }
        preM = preM.next;
    }
    
    //last preM and M may be null
    if (preM == null || preM.next == null) {
        return null;
    }
    
    //check preM, M
    ListNode M = preM.next, prev = M, cur = prev.next;
    
    for (int i = m; i < n; i++) {
        if (cur == null) { //cur possible null: check from M.next to N
            return null;
        }
        
        ListNode tmp = cur.next;
        cur.next = prev;
        prev = cur;
        cur = tmp;
    }
    preM.next = prev;
    M.next = cur;
    
    return dummy.next;
}
```
{% endtab %}
{% endtabs %}

