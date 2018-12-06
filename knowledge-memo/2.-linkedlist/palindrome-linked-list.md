---
description: Implement a function to check if a linked list is a palindrome.
---

# palindrome linked list

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    /**
     * @param head: A ListNode.
     * @return: A boolean.
     */
    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        
        //find the middle
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        //reverse the second half and compare with the first half
        slow = reverse(slow);
        fast = head;
        
        while (slow != null) {
            if (slow.val != fast.val) {
                return false;
            }
            
            slow = slow.next;
            fast = fast.next;
        }
        
        return true;
    }
    
    public ListNode reverse(ListNode node) {
        ListNode prev = null;
        while (node != null) {
            ListNode tmp = node.next;
            node.next = prev;
            prev = node;
            node = tmp;
        }
        
        return prev;
    }
}
```
{% endtab %}
{% endtabs %}

