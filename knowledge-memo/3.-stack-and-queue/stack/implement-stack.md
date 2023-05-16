# implement stack

{% tabs %}
{% tab title="Notes" %}
LinkedList or ArrayList or queues
{% endtab %}

{% tab title="Solution" %}
```java
public class Stack {
    class ListNode {
        int val;
        ListNode next;
        public ListNode(int val) {
            this.val = val;
            next = null;
        }
    }

    ListNode head;

    /*
     * @param x: An integer
     * @return: nothing
     */
    public void push(int x) {
        // write your code here
        ListNode node = new ListNode(x);
        node.next = head;
        head = node;
    }

    /*
     * @return: nothing
     */
    public void pop() {
        if (head == null) {
            return;
        }

        head = head.next;
    }

    /*
     * @return: An integer
     */
    public int top() {
        if (head == null) {
            return -1;
        }
        
        return head.val;
    }

    /*
     * @return: True if the stack is empty
     */
    public boolean isEmpty() {
        return head == null;
    }
}

```
{% endtab %}
{% endtabs %}
