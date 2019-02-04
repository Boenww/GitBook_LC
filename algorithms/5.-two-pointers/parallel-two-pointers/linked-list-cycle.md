# 141/142. linked list cycle I && II

## I

Given a linked list, determine if it has a cycle in it.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        
        ListNode slow = head, fast = head.next;
        while (slow != fast) {
            //!!! check fast also
            if (fast == null || fast.next == null) {
                return false;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return true;
    }
}
```
{% endtab %}
{% endtabs %}

## II

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
//Follow up
public ListNode detectCycle(ListNode head) {
    if (head == null || head.next == null) {
        return null;
    }
    
    ListNode slow = head, fast = head.next;
    while (slow != fast) {
        if (fast == null || fast.next == null) {
            return null;
        }
        
        slow = slow.next;
        fast = fast.next.next;
    }
    
    slow = head;
    fast = fast.next;
    while (slow != fast) {
        slow = slow.next;
        fast = fast.next;
    }
    
    return slow;
}
```
{% endtab %}
{% endtabs %}

