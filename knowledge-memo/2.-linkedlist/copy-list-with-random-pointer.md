# copy list with random pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

{% tabs %}
{% tab title="Notes" %}
* The lower copied list is wrong.

![](../../.gitbook/assets/image.png)

* O\(n\) space with hashmap
* O\(1\) space by traversing three times
{% endtab %}

{% tab title="Solution" %}
```java
public class Solution {
    //O(1) space
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        
        //1. copy next
        copyNext(head);
        
        //2. copy random
        copyRandom(head);
        
        //3. split
        return splitList(head);
    }
    
    private void copyNext(RandomListNode head) {
        while (head != null) {
            RandomListNode node = new RandomListNode(head.label);
            node.next = head.next;
            head.next = node;
            head = node.next;
        }
    }
    
    private void copyRandom(RandomListNode head) {
        while (head != null) {
            if (head.random != null) {
                head.next.random = head.random.next;    
            }
            
            head = head.next.next;
        }
    }
    
    private RandomListNode splitList(RandomListNode head) {
        RandomListNode res = head.next;
        while (head != null && head.next != null) {
            RandomListNode tmp = head.next;
            head.next = head.next.next;
            head = tmp;
        }
        
        return res;
    }
    
    //O(n) space with HashMap
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        
        Map<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode cur = head;
        while (cur != null) {
            map.put(cur, new RandomListNode(cur.label));
            cur = cur.next;
        }
        
        cur = head;
        while (cur != null) {
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }
        
        return map.get(head);
    }
}
```
{% endtab %}
{% endtabs %}

