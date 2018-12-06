# intersection of two linked lists

{% tabs %}
{% tab title="Notes" %}
* exchange starting positions
* link as a cycle: fast and slow pointers
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    //exchange starting positions
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        
        ListNode A = headA, B = headB;
        boolean noIntersection = false;
        while (true) {
            if (A == B) {
                return A;
            }
            
            if (A.next == null) {
                if (noIntersection) {
                    break;
                } else {
                    A = headB;
                    noIntersection = true;
                }
            } else {
                A = A.next;
            }
            
            B = B.next == null ? headA : B.next;
        }
        
        return null;
    }
    
    //link as a cycle
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        //corner case
        if (headA == null || headB == null) {
            return null;
        }
        
        ListNode head = headA;
        while (head.next != null) { //head.next!!!
            head = head.next;
        }
        head.next = headB;
        ListNode res = helper(headA);
        head.next = null;
        
        return res;
    }
    
    
    public ListNode helper(ListNode head) {
        ListNode slow = head, fast = head.next;
        
        while (slow != fast) {
            if (fast == null || fast.next == null) { //not linked as a cycle
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
}
```
{% endtab %}
{% endtabs %}

