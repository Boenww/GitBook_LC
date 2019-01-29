# partition lists

Given a linked list and a value _x_, partition it such that all nodes less than _x_ come before nodes greater than or equal to _x_.

You should preserve the original relative order of the nodes in each of the two partitions.

```text
Example:
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```

{% tabs %}
{% tab title="Notes" %}

{% endtab %}

{% tab title="Solution" %}
```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode leftHead = new ListNode(0), rightHead = new ListNode(0);
        ListNode left = leftHead, right = rightHead;
        while (head != null) {
            if (head.val < x) {
                left.next = head;
                left = left.next;
            } else {
                right.next = head;
                right = right.next;
            }
            head = head.next;
        }
        
        right.next = null;
        left.next = rightHead.next;
        
        return leftHead.next;
    }
}
```
{% endtab %}
{% endtabs %}

